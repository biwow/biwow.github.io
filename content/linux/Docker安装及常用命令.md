[TOC]

## 设置CentOS的源  

```
yum install -y yum-utils  
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo  
yum makecache fast
```
## 安装docker-ce(社区版)，EE版要收费的  
```
yum -y install docker-ce  
systemctl start docker  
# 加入开机自启动
systemctl enable docker  
```
## 启动docker没有镜像？
去https://hub.docker.com/search/去找一个，我在https://hub.docker.com/_/centos/ 找到了centos各个版本
```
docker pull centos //默认获取最新版本镜像  
docker pull centos:6.6 //获取centos6.6版本镜像
```
有可能运行会报错，网络或者中国防火墙的原因，所以我去GitHub手动下载的Dockerfile和镜像包，过程如下：
```
#vim Dockerfile  

FROM scratch
MAINTAINER https://github.com/CentOS/sig-cloud-instance-images
ADD centos-7-docker.tar.xz /

LABEL name="CentOS Base Image" \
    vendor="CentOS" \
    license="GPLv2" \
    build-date="20170315"

CMD ["/bin/bash"]
```
```
#下载镜像包
wget https://raw.githubusercontent.com/CentOS/sig-cloud-instance-images/3463e5f011fbd82f8283757408427802ee020ee4/docker/centos-7-docker.tar.xz    
#使用该Dockerfile和镜像包构建docker镜像
docker build -t centos:7 .    
#查看所有可用镜像，之前构建的镜像就可以看到了
docker images   

docker create -ti --name "nodejs" centos:7 bash //利用centos:7镜像创建容器  
docker ps -a  //查看所有容器  
docker start -ai nodejs  //启动创建的nodejs容器   
docker attach nodejs  //进入容器  
docker exec -it nodejs bash //进入容器  
docker commit nodejs lqb/nodejs:1 //原有容器生成镜像  
[ctrl + P][ctrl + Q]退出而不终止容器  
docker export 20ba1c4c4fe6 > nodejs.tar //导出容器到本地
docker load < nodejs.tar  
结论：save只能对image用，产生的文件需要用load来生成image；export的对象是container，产生的文件需要用import来生成image。

docker start $(docker ps -a | awk '{ print $1}' | tail -n +2) //启动所有容器  

cat nodejs.tar | docker import - lqb/nodejs:2 //导入本地文件到镜像  
docker run -i -t -p 8080:8080 --name "nodejs" lqb/nodejs:1.1 /bin/bash  //使用镜像创建容器监听端口
```
//更改docker存储位置
```
docker info | grep "Root Dir"  查看存储  
rsync -avP /var/lib/docker/ /data/docker/   
mv docker docker_bak  
ln -s /data/docker /var/lib/docker
```
我们可以通过修改 docker daemon的配置文件的方式来保存我们修改，方法如下：

默认情况下，docker daemon 会有一个默认的configuration 文件，此外，我们可以新建一个名为“daemon.json”文件的文件，我们在这个文件中的定义，会覆盖默认配置文件的内容文件。

```
#cd etc/docker
#vim daemon.json
在这个文件里面加入我们的内容，即修改docker daemon 的 Rootpath

{
    "graph": "/data/docker"
}
重新 load 配置

systemctl daemon-reload
重新启动 docker daemon

systemctl restart docker.service
```

```
docker run -d -i -t -p 1011:80 -v /data/deposit/credit2go:/data/credit2go --name "credit2go" lqb/nodejs:328 /bin/bash //创建 监听端口并挂载  

docker run -itd --restart=unless-stopped -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone -p 8811:8811 --add-host vip.gh.com:172.17.67.8 --name xianfeng-pay --workdir=/data -d harbor.guohuaitech.com/mimosa/gh-mimosa-boot:1.5.2   

docker run -i -t -p 1000:80 -v /data/deposit/api:/data/api --name "api" lqb/nodejs:1.1 /bin/bash
```
## docker 增加端口映射
```
docker inspect `container_name` | grep IPAddress  //查看容器对应的ip地址
iptables -t nat --list-rules DOCKER  //查看docker所有端口映射
iptables -t nat --list-rules DOCKER |grep "172.17.0.12" //查看对应ip地址的端口映射
docker commit containerid foo/live  //当前容器生成镜像
docker run -i -t -p 1000:80 -v /data:/data --name "api" foo/live /bin/bash  //用镜像生成容器
```
## Operation not permitted
```
docker run -itd --restart=unless-stopped -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone -p 0.0.0.0:8899:8899 -p 0.0.0.0:50000:50000 --add-host vip.gh.com:172.17.67.8 --name mimosa -v /data/docker_mount/mimosa:/data -d harbor.guohuaitech.com/mimosa/gh-mimosa-boot:1.5.2 /usr/sbin/init
```
> vim Dockerfile

```
FROM lqb/nodejs:1.1
RUN yum -y update
RUN yum install -y vim
ENV NODE_HOME /usr/local/nodejs
ENV PATH $PATH:$NODE_HOME/bin
ENV NODE_PATH $NODE_HOME/lib/node_modules
CMD ["source","/etc/profile"]
```
> docker build --rm=true -t="lqb/nodejs:1.2" .    //利用Dockerfile创建新镜像

> vim Dockerfile

```
FROM java:8-jdk-alpine
WORKDIR /data
CMD /data/start.sh
```
> docker build --rm=true -t="ssth/java8" .    //利用Dockerfile创建新镜像

====================================================

> docker save -o nodejs.tar lqb/nodejs:1.1 //保存镜像  
> docker load < nodejs.tar  //导入本地镜像
> docker commit nodejs lqb/nodejs:1 //原有容器生成镜像

====================================================  
> docker logs -f esb  //查看容器日志  
> docker inspect esb  //查看容器详细信息  
> docker cp linux.sh esb:/root/  //容器之间内容拷贝
> docker diff esb  //容器和镜像对比区别 
> docker port esb 80 //查看映射端口配置
================================================  
> docker login  //登录https://hub.docker.com  
> docker search nodejs  //查找官网镜像  
> docker pull readytalk/nodejs  //下载镜像到本地  
> docker login  
> docker tag lqb/nodejs:1.2 biwow/nodejs:1.2 //镜像名称与官网名称一致  
> docker push biwow/nodejs:1.2 //发布镜像到官网

## Docker中容器无法停止无法删除
```
1.停止所有的容器  
docker stop $(docker ps -q)  
2.强制移除此容器  
docker rm -f mysql1  
3.清理此容器的网络占用  
格式：docker network disconnect --force 网络模式 容器名称  
示例：docker network disconnect --force bridge mysql1  
4.简查是否还有同名容器占用  
格式：docker network inspect 网络模式  
示例：docker network inspect bridge  
# Add additional binaries into PATH for convenience
ENV PATH=$PATH:/usr/local/openresty/nginx/sbin
```
