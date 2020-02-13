#### 1、基础知识
##### 1.1、名词解释
###### 1.1.1、什么是PKI
公钥基础设施（Public Key Infrastructure，PKI）是一种遵循标准的利用公钥加密技术为电子商务的开展提供一套安全基础平台的技术和规范。一个机构通过采用PKI 框架管理密钥和证书可以建立一个安全的网络环境。  
PKI 主要包括四个部分：
- X.509 格式的证书（X.509 V3）和证书废止列表CRL（X.509 V2）
- CA 操作协议
- CA 管理协议
- CA 政策制定
###### 1.1.2、什么是ACL
访问控制列表（Access Control List，ACL） 是路由器和交换机接口的指令列表，用来控制端口进出的数据包。
###### 1.1.3、什么是fabric
以区块链为底层的分布式账本
###### 1.1.4、什么是MSP
成员服务提供者（Membership Service Providers，MSP） 是区块链网络中用于颁发和验证证书和身份的一组加密机制和协议。
###### 1.1.5、什么是ECDSA
椭圆曲线数字签名算法（ECDSA）是使用椭圆曲线密码（ECC）对数字签名算法（DSA）的模拟。
###### 1.1.6、什么是CSR
证书请求文件（Certificate Signing Request，CSR） 是证书申请者在申请数字证书时由CSP(加密服务提供者)在生成私钥的同时也生成证书请求文件，证书申请者只要把CSR文件提交给证书颁发机构后，证书颁发机构使用其根证书私钥签名就生成了证书公钥文件，也就是颁发给用户的证书。
##### 1.2、fabric期望解决的问题
为了解决这种“信任”问题而产生的技术，在双方进行交易的同时对数据进行了认证，那么便无需交易后再进行清算而达到实时转账等功能。
##### 1.3、fabric关键节点
节点名称 | 节点说明
---|---
Peer节点 | 该节点是参与交易的主体，负责储存完整的账本数据即区块链数据，负责共识环节中的执行智能合约
Orderer节点 | 该节点负责收集交易请求进行排序并打包生产新的区块，主体功能便是对交易排序从而保证各Peer节点上的数据一致性，也包含了ACL进行访问控制
CA节点 | 该节点负责对加入链内的所有节点进行授权认证，包括上层的client端，每一个节点都有其颁发的证书用于交易流程中的身份识别
Client端 | 提供了SDK让开发人员可以更容易地对接到区块链内的交易环节
##### 1.4 fabric知识结构
![image](https://images2018.cnblogs.com/blog/1240530/201806/1240530-20180609231606031-1388017672.jpg)
#### 2、成员服务提供者 Membership Service Providers(MSP)
##### 2.1 MSP目录
![image](http://biwow.com/asset/wiki/fabric/msp_folder.png)
##### 2.2、MSP主要应用场景
- 在部署智能合约或者初始化时需要拥有对应CA赋权的证书才可执行（默认为PeerAdmin用户）
- 为新节点或用户注册证书时，需要CA对该操作证书赋予权限（一般为Admin用户）
- 在背书策略中可通过MSP来代表背书成员，可设定单个Peer节点代表其MSP达成协议（也可以要求全部Peer节点通过才达成协议）
- 在跨MSP间的Peer节点通信，先通过各MSP内指定的Anchor Peer收集MSP内的Peer列表，然后通过各MSP下的Anchor Peer交互其Peer列表，将其他MSP下的Peer列表同步到内部Peer后，便通过Gossip协议Peer节点间随机通信
- 每个MSP都有自己独立的CA节点，为其提供所有的证书需求，各MSP共享其CA节点的ROOT证书达到互相认证
- Revoke，废除证书。在PKI体系中，其最大的优势便是Off line的，即在证书颁发后，不需要CA节点的存在也可以在本地进行认证，而遇到很大的问题是类似于废除证书时如果希望能即是将废除证书的消息通知到各个节点，目前的做法是需要CA节点保持在线并与各节点保持通信
##### 2.3、节点签名
如果需要设置签名者MSP，需要将下面四组文件复制到节点文件系统中的专用位置，四组文件为：
- Cacert – PEM文件，MSP的根证书,使用PKI(Public Key Infrastructure)等数字签名技术用于识别客户身份
- Admincerts – PEM文件，MSP的管理员证书
- Keystore-  节点的签名私钥
- Signcerts – PEM文件，节点身份的编码证书，fabric有四种身份:user，peer， orderer，client

#### 3、账户创建
##### 3.1 身份注册的预置属性
属性名 | 类型 | 描述
---|---|---
hf.Registrar.Roles | List | 注册者可以管理的角色列表
hf.Registrar.DelegateRoles | List | 注册者可以授予被注册身份hf.Registrar.Roles属性的角色列表
hf.Registrar.Attributes | List | 注册者允许注册的属性列表
hf.GenCRL | Boolean | 如果true则身份可以生成CRL
hf.Revoker | Boolean | 如果true则身份可以撤销用户或证书
hf.AffiliationMgr | Boolean | 如果true则身份可以管理组织关系
hf.IntermediateCA | Boolean | 如果true则身份可以登记中间CA Server
##### 3.2 账户创建
以admin身份证书注册了一个id为admin2，组织关系为org1.department1的用户，并提供了hf.Revoker的保留属性和admin的自定义属性（:ecert表示该属性名和值会插入到登记证书中）
```
export FABRIC_CA_CLIENT_HOME=$HOME/fabric-ca/clients/admin
fabric-ca-client register --id.name admin2 --id.affiliation org1.department1 --id.attrs 'hf.Revoker=true,admin=true:ecert'
```
以user身份证书注册了一个id为user1,密码为user1pw，组织关系为org1的用户
```
fabric-ca-client register --id.name user1 --id.secret user1pw --id.type user --id.affiliation org1 --id.attrs 'hf.Affiliation=org1:ecert,email=user1@gmail.com'
```
##### 3.3 登记身份
```
fabric-ca-client enroll -u http://user1:user1pw@localhost:7054 --enrollment.attrs "email:opt"
```
##### 3.4 修改密码
```
fabric-ca-client identity modify user1 --secret newpass --type peer
```
##### 3.5 删除用户
```
fabric-ca-client identity remove user1
```
注意：在默认情况下，Fabric CA服务器是禁用身份的删除的，但可以通过设置–cfg.identities.allowremove选项启动Fabric CA服务器启用。