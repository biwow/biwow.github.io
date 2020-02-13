#### 目录
* [安装git](#安装git)
* [安装Docker Compose](#Compose)
* [安装golang](#安装golang)
* [fabric资源下载](#fabric资源下载)
* [部署fabric](#部署fabric)

<!------------这是分隔符------------> 
#### 安装git
```
yum install -y git
```
<!------------这是分隔符------------> 
#### <span id="Compose">安装Docker Compose</span>
```
curl -L https://get.daocloud.io/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` > /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
<!------------这是分隔符------------> 
#### 安装golang
```
wget https://studygolang.com/dl/golang/go1.9.3.linux-amd64.tar.gz  
tar -zvxf go1.9.3.linux-amd64.tar.gz -C /usr/local/  
mkdir /mnt/golang    
# /etc/profile
export GOROOT=/usr/local/go
export GOBIN=$GOROOT/bin
export GOPKG=$GOROOT/pkg/tool/linux_amd64
export GOARCH=amd64
export GOOS=linux
export GOPATH=/mnt/golang
export PATH=$PATH:$GOBIN:$GOPKG:$GOPATH/bin

source /etc/profile
go version
```
<!------------这是分隔符------------> 
#### fabric资源下载
* [快捷下载](#快捷下载)
* [二进制文件下载](#二进制文件下载)
* [下载镜像](#下载镜像)

<!------------这是分隔符------------> 
##### 快捷下载
```
curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/release-1.3/scripts/bootstrap.sh | bash -s <fabric> <fabric-ca> <thirdparty>
curl -sSL https://raw.githubusercontent.com/hyperledger/fabric/release-1.3/scripts/bootstrap.sh | bash -s 1.3.0 1.3.0 0.4.13
```
[^_^]:
    备用地址
    https://raw.githubusercontent.com/hyperledger/fabric/master/scripts/bootstrap.sh
    https://raw.githubusercontent.com/hyperledger/fabric/release-1.3/scripts/bootstrap.sh
<!------------这是分隔符------------> 
##### 二进制文件下载
```
wget https://nexus.hyperledger.org/content/repositories/releases/org/hyperledger/fabric/hyperledger-fabric/linux-amd64-1.3.0/hyperledger-fabric-linux-amd64-1.3.0.tar.gz
wget https://nexus.hyperledger.org/content/repositories/releases/org/hyperledger/fabric-ca/hyperledger-fabric-ca/linux-amd64-1.3.0/hyperledger-fabric-ca-linux-amd64-1.3.0.tar.gz
```
可执行命令的作用：
名称 | 作用
---|---
peer | 负责启动节点，存储区块链数据，运行维护链码
order | 负责启动排序节点，对交易进行排序，并将排序好的交易打包成模块
cryptogen | 生成组织结构和身份文件
configtxgen | 生成配置区块和配置交易
configtxlator | 解读配置信息
##### 下载镜像
```
//fabric相关镜像
docker pull hyperledger/fabric-peer:1.3.0
docker pull hyperledger/fabric-orderer:1.3.0
docker pull hyperledger/fabric-ccenv:1.3.0
docker pull hyperledger/fabric-tools:1.3.0
//ca相关镜像
docker pull hyperledger/fabric-ca:1.3.0
//第三方相关镜像
docker pull hyperledger/fabric-couchdb:0.4.14
docker pull hyperledger/fabric-kafka:0.4.14
docker pull hyperledger/fabric-zookeeper:0.4.14
```
镜像说明如下：
镜像名称 | 是否可选 | 镜像说明
---|---|---
hyperledger/fabric-tools | 可选 | 包含crytogen、configtxgen、configtxlator我第二次工具的镜像文件
hyperledger/fabric-couchdb | 可选 | CouchDB的数据库镜像文件、状态数据库选择CouchDB的时候才需要
hyperledger/fabric-kafka | 可选 | Kafka的镜像文件
hyperledger/fabric-zookeeper | 可选 | Zookeeper的镜像文件
hyperledger/fabric-peer | 必选 | Peer节点的镜像文件
hyperledger/fabric-orderer | 必选 | 排序服务节点的镜像文件
hyperledger/fabric-javaenv | 可选 | java链码的基础镜像文件
hyperledger/fabric-ccenv | 必选 | Golang链码的基础镜像文件
hyperledger/fabric-ca | 可选 | fabric-ca的镜像文件，用到fabric-ca的时候才需要

<!------------这是分隔符------------> 
#### 部署fabric
* [生成组织节点文件信息](#生成组织节点文件信息)
* [生成Orderer服务启动的初始区块](#生成orderer服务启动的初始区块)
* [生成新建应用通道的配置交易文件](#生成新建应用通道的配置交易文件)
* [生成锚节点配置更新文件](#生成锚节点配置更新文件)
* [创建通道](#创建通道)
* [Peer节点加入指定通道](#Peer节点加入指定通道)
* [为频道中的每个组织设置Peer节点](#为频道中的每个组织设置Peer节点)
* [在节点上安装智能合约](#在节点上安装智能合约)
* [在节点上对智能合约进行实例化操作](#在节点上对智能合约进行实例化操作)
* [在节点上执行智能合约中的查询方法](#在节点上执行智能合约中的查询方法)
* [在节点上执行智能合约中的交易方法](#在节点上执行智能合约中的交易方法)


<!------------这是分隔符------------> 
##### 生成组织节点文件信息
```
cryptogen generate --config=./crypto-config.yaml
```

<!------------这是分隔符------------> 
##### 生成Orderer服务启动的初始区块
```
configtxgen -profile TwoOrgsOrdererGenesis -outputBlock ./channel-artifacts/genesis.block
```
<!------------这是分隔符------------> 
##### 生成新建应用通道的配置交易文件
```
configtxgen -profile TwoOrgsChannel -outputCreateChannelTx ./channel-artifacts/channel.tx -channelID mychannel
```

<!------------这是分隔符------------> 
##### 生成锚节点配置更新文件
```
configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org1MSPanchors.tx -channelID mychannel -asOrg Org1MSP  
configtxgen -profile TwoOrgsChannel -outputAnchorPeersUpdate ./channel-artifacts/Org2MSPanchors.tx -channelID mychannel -asOrg Org2MSP
```

<!------------这是分隔符------------> 
##### 创建通道
```
peer channel create -o orderer.example.com:7050 (指定排序服务地址) -c $CHANNEL_NAME (频道名称) -f ./channel-artifacts/channel.tx (当前频道创建之前所绑定的频道文件)
```

<!------------这是分隔符------------> 
##### Peer节点加入指定通道
```
peer channel join -b $CHANNEL_NAME.block >&log.txt
```

<!------------这是分隔符------------> 
##### 为频道中的每个组织设置Peer节点
```
peer channel join -b $CHANNEL_NAME.block >&log.txt
```

<!------------这是分隔符------------> 
##### 在节点上安装智能合约
```
peer chaincode install -n mycc -v ${VERSION} -l ${LANGUAGE} -p ${CC_SRC_PATH} >&log.txt
```

<!------------这是分隔符------------> 
##### 在节点上对智能合约进行实例化操作
背书即对当前合约执行写入的权限控制方案
```
peer chaincode instantiate -o orderer.example.com:7050 -C $CHANNEL_NAME -n mycc -l ${LANGUAGE} -v ${VERSION} -c '{"Args":["init","a","100","b","200"]}' -P "AND ('Org1MSP.peer','Org2MSP.peer')" >&log.txt
```

<!------------这是分隔符------------> 
##### 在节点上执行智能合约中的查询方法
```
peer chaincode query -C $CHANNEL_NAME -n mycc -c '{"Args":["query","a"]}' >&log.txt
```

<!------------这是分隔符------------> 
##### 在节点上执行智能合约中的交易方法
```
peer chaincode invoke -o orderer.example.com:7050 -C $CHANNEL_NAME -n mycc $PEER_CONN_PARMS -c '{"Args":["invoke","a","b","10"]}' >&log.txt
```