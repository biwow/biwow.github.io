[TOC]
## 参考文档
```
https://kubernetes.io/zh/docs/
https://preliminary.istio.io/zh/docs/
https://github.com/istio/istio
```
## 整体架构
![image](https://www.kubernetes.org.cn/img/2018/07/20180713203443.jpg)

Kubernetes属于主从分布式架构，主要由Master Node和Worker Node组成，以及包括客户端命令行工具kubectl和其它附加项。
> Master Node：作为控制节点，对集群进行调度管理；Master Node由API Server、Scheduler、Cluster State Store和Controller-Manger Server所组成；
- **API Server（API服务器）**  
API Server主要用来处理REST的操作，确保它们生效，并执行相关业务逻辑，以及更新etcd（或者其他存储）中的相关对象。API Server是所有REST命令的入口，它的相关结果状态将被保存在etcd（或其他存储）中。
- **Cluster state store（集群状态存储）**  
Kubernetes默认使用etcd作为集群整体存储，当然也可以使用其它的技术。etcd是一个简单的、分布式的、一致的key-value存储，主要被用来共享配置和服务发现。etcd提供了一个CRUD操作的REST API，以及提供了作为注册的接口，以监控指定的Node。集群的所有状态都存储在etcd实例中，并具有监控的能力，因此当etcd中的信息发生变化时，就能够快速的通知集群中相关的组件。
- **Controller-Manager Server（控制管理服务器）**  
Controller-Manager Serve用于执行大部分的集群层次的功能，它既执行生命周期功能(例如：命名空间创建和生命周期、事件垃圾收集、已终止垃圾收集、级联删除垃圾收集、node垃圾收集)，也执行API业务逻辑（例如：pod的弹性扩容）。控制管理提供自愈能力、扩容、应用生命周期管理、服务发现、路由、服务绑定和提供。Kubernetes默认提供Replication Controller、Node Controller、Namespace Controller、Service Controller、Endpoints Controller、Persistent Controller、DaemonSet Controller等控制器。
- **Scheduler（调度器）**  
scheduler组件为容器自动选择运行的主机。依据请求资源的可用性，服务请求的质量等约束条件，scheduler监控未绑定的pod，并将其绑定至特定的node节点。Kubernetes也支持用户自己提供的调度器，Scheduler负责根据调度策略自动将Pod部署到合适Node中，调度策略分为预选策略和优选策略。


> Worker Node：作为真正的工作节点，运行业务应用的容器；Worker Node包含kubelet、kube proxy和Container Runtime；

- **Kubelet**  
Kubelet是Kubernetes中最主要的控制器，它是Pod和Node API的主要实现者，Kubelet负责驱动容器执行层。在Kubernetes中，应用容器彼此是隔离的，并且与运行其的主机也是隔离的，这是对应用进行独立解耦管理的关键点。在Kubernets中，Pod作为基本的执行单元，它可以拥有多个容器和存储数据卷，能够方便在每个容器中打包一个单一的应用，从而解耦了应用构建时和部署时的所关心的事项，已经能够方便在物理机/虚拟机之间进行迁移。API准入控制可以拒绝或者Pod，或者为Pod添加额外的调度约束，但是Kubelet才是Pod是否能够运行在特定Node上的最终裁决者，而不是scheduler或者DaemonSet。kubelet默认情况使用cAdvisor进行资源监控。负责管理Pod、容器、镜像、数据卷等，实现集群对节点的管理，并将容器的运行状态汇报给Kubernetes API Server。
- Container Runtime（容器运行时）  
每一个Node都会运行一个Container Runtime，其负责下载镜像和运行容器。Kubernetes本身并不停容器运行时环境，但提供了接口，可以插入所选择的容器运行时环境。kubelet使用Unix socket之上的gRPC框架与容器运行时进行通信，kubelet作为客户端，而CRI shim作为服务器。
![image](https://img-blog.csdn.net/20180604215822299?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3UwMTQwNDIzNzI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
protocol buffers API提供两个gRPC服务，ImageService和RuntimeService。ImageService提供拉取、查看、和移除镜像的RPC。RuntimeSerivce则提供管理Pods和容器生命周期管理的RPC，以及与容器进行交互(exec/attach/port-forward)。容器运行时能够同时管理镜像和容器（例如：Docker和Rkt），并且可以通过同一个套接字提供这两种服务。在Kubelet中，这个套接字通过–container-runtime-endpoint和–image-service-endpoint字段进行设置。Kubernetes CRI支持的容器运行时包括docker、rkt、cri-o、frankti、kata-containers和clear-containers等。
- **kube proxy**  
基于一种公共访问策略（例如：负载均衡），服务提供了一种访问一群pod的途径。此方式通过创建一个虚拟的IP来实现，客户端能够访问此IP，并能够将服务透明的代理至Pod。每一个Node都会运行一个kube-proxy，kube proxy通过iptables规则引导访问至服务IP，并将重定向至正确的后端应用，通过这种方式kube-proxy提供了一个高可用的负载均衡解决方案。服务发现主要通过DNS实现。在Kubernetes中，kube proxy负责为Pod创建代理服务；引到访问至服务；并实现服务到Pod的路由和转发，以及通过应用的负载均衡。

> kubectl：kubectl是Kubernetes集群的命令行接口。用于通过命令行与API Server进行交互，而对Kubernetes进行操作，实现在集群中进行各种资源的增删改查等操作；

> Add-on：是对Kubernetes核心功能的扩展，例如增加网络和网络策略等能力。

> 附加项和其他依赖

在Kunbernetes中可以以附加项的方式扩展Kubernetes的功能，目前主要有网络、服务发现和可视化这三大类的附加项，下面是可用的一些附加项：  
- **网络和网络策略**  
ACI 通过与Cisco ACI集成的容器网络和网络安全。  
Calico 是一个安全的3层网络和网络策略提供者。  
Canal 联合Fannel和Calico，通过网络和网络侧。  
Cilium 是一个3层网络和网络侧插件，它能够透明的加强HTTP/API/L7策略。其即支持路由，也支持overlay/encapsultion模式。  
Flannel 是一个overlay的网络提供者。  
- **服务发现**  
CoreDNS 是一个灵活的，可扩展的DNS服务器，它能够作为Pod集群内的DNS进行安装。   
Ingress 提供基于Http协议的路由转发机制。
- **可视化&控制**  
Dashboard 是Kubernetes的web用户界面。

#### 第一步 安装k8s
确保每个节点上 MAC 地址和 product_uuid 的唯一性
```
# 查看MAC
ifconfig -a
# 查看product_uuid
cat /sys/class/dmi/id/product_uuid
```
主机名设置
```
#master节点
hostnamectl  set-hostname  master && exec bash 
#node1节点
hostnamectl  set-hostname  node1 && exec bash 
#node2节点
hostnamectl  set-hostname  node2 && exec bash 
```
hosts文件设置
```
10.4.3.91 master 
10.4.3.81 node1 
10.4.3.82 node2
```
防火墙和selinux设置
```
# 关闭SELINUX服务
sed -i "s/^SELINUX\=enforcing/SELINUX\=disabled/g" /etc/selinux/config
# 关闭selinux防火墙
setenforce 0 
# 关闭防火墙
systemctl stop firewalld 
# 禁止防火墙开机启动
systemctl disable firewalld
```
避免iptables 被绕过导致网络请求被错误的路由
```
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
sysctl --system
# 查看ip_forward是否为1，如果不为1则修改
cat /proc/sys/net/ipv4/ip_forward
cat <<EOF >  /etc/sysctl.d/k8s.conf
net.ipv4.ip_forward = 1
EOF
sysctl --system
```
设置yum源
```
cat <<EOF > /etc/yum.repos.d/kubernetes.repo
[kubernetes]
name=Kubernetes
baseurl=http://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64
enabled=1
gpgcheck=0
repo_gpgcheck=0
gpgkey=http://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg
        http://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg
EOF
```
yum 安装
```
yum install -y kubelet kubeadm kubectl --disableexcludes=kubernetes
```
设置开机自启动
```
systemctl enable kubelet
```
拉取镜像
```
docker pull k8s.gcr.io/kube-apiserver:v1.13.4
docker pull k8s.gcr.io/kube-controller-manager:v1.13.4
docker pull k8s.gcr.io/kube-scheduler:v1.13.4
docker pull k8s.gcr.io/kube-proxy:v1.13.4
docker pull k8s.gcr.io/pause:3.1
docker pull k8s.gcr.io/etcd:3.2.24
docker pull k8s.gcr.io/coredns:1.2.6
```

如果不能翻墙，参考一下操作
```
# 拉取其他镜像容器
docker pull biwow/kube-apiserver:v1.13.4
docker pull biwow/kube-controller-manager:v1.13.4
docker pull biwow/kube-scheduler:v1.13.4
docker pull biwow/kube-proxy:v1.13.4
docker pull biwow/pause:3.1
docker pull biwow/etcd:3.2.24
docker pull biwow/coredns:1.2.6
# 命令合并：docker pull biwow/kube-apiserver:v1.13.4;docker pull biwow/kube-controller-manager:v1.13.4;docker pull biwow/kube-scheduler:v1.13.4;docker pull biwow/kube-proxy:v1.13.4;docker pull biwow/pause:3.1;docker pull biwow/etcd:3.2.24;docker pull biwow/coredns:1.2.6
# 修改镜像名称为官方使用的名称
docker tag biwow/kube-apiserver:v1.13.4 k8s.gcr.io/kube-apiserver:v1.13.4
docker tag biwow/kube-controller-manager:v1.13.4 k8s.gcr.io/kube-controller-manager:v1.13.4
docker tag biwow/kube-scheduler:v1.13.4 k8s.gcr.io/kube-scheduler:v1.13.4
docker tag biwow/kube-proxy:v1.13.4 k8s.gcr.io/kube-proxy:v1.13.4
docker tag biwow/pause:3.1 k8s.gcr.io/pause:3.1
docker tag biwow/etcd:3.2.24 k8s.gcr.io/etcd:3.2.24
docker tag biwow/coredns:1.2.6 k8s.gcr.io/coredns:1.2.6
# 命令合并：docker tag biwow/kube-apiserver:v1.13.4 k8s.gcr.io/kube-apiserver:v1.13.4;docker tag biwow/kube-controller-manager:v1.13.4 k8s.gcr.io/kube-controller-manager:v1.13.4;docker tag biwow/kube-scheduler:v1.13.4 k8s.gcr.io/kube-scheduler:v1.13.4;docker tag biwow/kube-proxy:v1.13.4 k8s.gcr.io/kube-proxy:v1.13.4;docker tag biwow/pause:3.1 k8s.gcr.io/pause:3.1;docker tag biwow/etcd:3.2.24 k8s.gcr.io/etcd:3.2.24;docker tag biwow/coredns:1.2.6 k8s.gcr.io/coredns:1.2.6
```
初始化一个 Kubernetes master 节点
```
kubeadm init --apiserver-advertise-address=自己IP  --pod-network-cidr=10.244.0.0/16

# 成功结果如下
Your Kubernetes master has initialized successfully!

To start using your cluster, you need to run the following as a regular user:

  mkdir -p $HOME/.kube
  sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
  sudo chown $(id -u):$(id -g) $HOME/.kube/config

You should now deploy a pod network to the cluster.
Run "kubectl apply -f [podnetwork].yaml" with one of the options listed at:
  https://kubernetes.io/docs/concepts/cluster-administration/addons/

You can now join any number of machines by running the following on each node
as root:

  kubeadm join 172.17.225.9:6443 --token lf6xra.ki17oh6ucw57152m --discovery-token-ca-cert-hash sha256:dab87ddbd03eb09b8e1f6598aa566de84cad119777a73c296814730d5cb5309e
  
# 请备份好输出中的kubeadm join 命令，因为您会需要这个命令来给集群添加节点

```
工具包功能说明
```
kubeadm: 用来初始化集群的指令
kubelet: 在集群中的每个节点上用来启动 pod 和 container 等
kubectl: 用来与集群通信的命令行工具
```
启动kubelet
```
systemctl start kubelet
```
添加环境变量
```
export KUBECONFIG=/etc/kubernetes/admin.conf
```
查看kubelet 启动情况
```
journalctl -xefu kubelet
# 错误：network plugin is not ready: cni config uninitialized
# 解决办法：创建 flannel的pod
kubectl apply -f  https://raw.githubusercontent.com/coreos/flannel/master/Documentation/kube-flannel.yml
```
# 补充/run/flannel/subnet.env文件
```
cat <<EOF >  /run/flannel/subnet.env
FLANNEL_NETWORK=10.244.0.0/16
FLANNEL_SUBNET=10.244.0.1/24
FLANNEL_MTU=1450
FLANNEL_IPMASQ=true
EOF
```
完成认证
```
# 通过命令查看都为running
kubectl get pods -n kube-system -w
```
- 修改默认nodePort端口号范围
```
# vim /etc/kubernetes/manifests/kube-apiserver.yaml,在command下添加参数.然后重启容器
–service-node-port-range=80-65530
```
#### k8s 常用命令
Pod:所有业务类型的基础，它是一个或多个容器的组合。这些容器共享存储、网络和命名空间，以及如何运行的规范。
```
kubectl get pods --all-namespaces -o wide //获取所有的pod
kubectl create -f YAML_FILE.yaml  //使用yaml文件创建pod
kubectl delete -f YAML_FILE.yaml  //使用yaml文件删除pod
kubectl logs POD_NAME -n kube-system  //显示指定命名空间的pod的日志
kubectl delete pod my-nginx-mq29p   //删除指定pod
kubectl describe pod my-nginx-ntvw5 //查看pod信息
kubectl exec -ti <pod-name> -n <namespace> sh   //进入pod
kubectl scale service/pod --replicas=4  //扩容或缩容pod数量
```
服务
```
kubectl get svc -n kube-system  //获取指定命名空间的服务
```
集群
```
kubectl cluster-info    //获取集群信息
kubectl get cs          //获取集群节点信息
kubectl get nodes  //获取全部节点
kubectl delete node 192.168.2.152  //删除节点
kubeadm token create --print-join-command   //生成新的添加节点命令
```
删除节点中的node
```
# 在master节点上执行
kubectl drain NODE_NAME --delete-local-data --force --ignore-daemonsets
kubectl delete node node1
# 在node节点上执行
kubeadm reset
ifconfig cni0 down
ip link delete cni0
ifconfig flannel.1 down
ip link delete flannel.1
rm -rf /var/lib/cni/
```
其他
```
# 输出指定的一个/多个资源的详细信息
kubectl describe pods
# 查看token
kubeadm token list
# 查看版本
kubelet --version
# 查看kubeadm版本
kubeadm version
# 查看kubeadm依赖包
kubeadm config images list
# 设置master也可以被调度
kubectl taint nodes --all node-role.kubernetes.io/master-
# 进入容器内部
kubectl exec -it name-xxxxx /bin/bash
# 创建镜像的秘钥
kubectl create secret docker-registry regsecret -n namespace --docker-server=registry-internal.cn-hangzhou.aliyuncs.com --docker-username=abc@aliyun.c
# 查看文件
kubectl get pods -o yaml
# 查看配置
kubeadm config view
#使用proxy，这样集群外部就能访问到集群内部的服务啦
kubectl proxy --address 0.0.0.0 --accept-hosts '.*'
# 查看配置文件
kubectl config view
```
#### 第二步 使用kubernetes创建一个简单项目
- 编写项目yaml文件
```
# vim nginx.yaml
apiVersion: v1              #必选，版本号
kind: ReplicationController            #必选，创建的是Pod，资源类型可以是Deployment、Job、Ingress、Service等。
metadata:                   #必选，元数据
  name: my-nginx    #必选，Pod名称
spec:                       #必选，Pod中容器的详细定义
  replicas: 2               #设置Pod的具体数量
  template:                 #设置Pod的模板
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx         #必选，容器名称
        image: nginx        #必选，容器的镜像名称
        ports:
        - containerPort: 80 #需要暴露的端口库号列表
---
apiVersion: v1
kind: Service
metadata:
  name: slb
spec:
  type: NodePort
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
    nodePort: 31111          #端口默认必须是30000-32767
  selector:
    app: nginx
```
- 使用配置文件创建实例
```
kubectl apply -f nginx.yaml
```
- 查看启动的pods信息
```
kubectl get pods --all-namespaces -o wide
```
- 可以尝试访问其中一个pod，会返回nginx信息
```
curl http://10.244.0.10
```
kubectl expose pods nginx-pod --type=NodePort

===================================================================
#### 第二步 安装istio
- 下载当前istio最新版本
```
# 下载压缩包
wget https://github.com/istio/istio/releases/download/1.1.0-rc.2/istio-1.1.0-rc.2-linux.tar.gz
tar zxvf istio-1.1.0-rc.2-linux.tar.gz
cd istio-1.1.0-rc.2
# 部署istio，第一次会有'unable to recognize'的错误，再次执行就好了
kubectl apply -f install/kubernetes/istio-demo.yaml
# 查看istio的容器
kubectl get pods -n istio-system -w
```

#### 第三步 运行istio的helloworld例子
这个示例运行一个简单helloworld服务的两个版本，在调用时返回它们的版本和实例(主机名)。它用于演示与自动伸缩结合使用的金丝雀部署。

- 手动注入sidecar
```
# 查看注入相关configmap是否已创建成功
kubectl get cm -n istio-system | grep istio-sidecar-injector
# 在原始内容的基础上加入sidecar的配置内容
istioctl kube-inject -f helloworld.yaml -o helloworld-istio.yaml
# 部署到kubernetes上
kubectl apply -f <(istioctl kube-inject -f helloworld.yaml)
# 查看pod详细内容
kubectl describe pod test-c9f4b55c7-np4cf
kubectl create -f helloworld-istio.yaml
kubectl create -f helloworld-gateway.yaml
```

#### 第三步 使用abi生成go文件调用智能合约的go文件
```
abigen --abi Storage.abi --pkg contract --out storage.go
```

命令 | 解释
---|---
--abi | 指定abi文件来源
--pkg | 指定输出文件的包名
--type | 指定合约结构体名称
--out | 指定合约交互文件名称