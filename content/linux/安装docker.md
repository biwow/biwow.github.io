## 安装docker
* [增加docker源](#增加docker源)
* [安装docker-ce(社区版)](#安装docker-ce)
* [增加docker开机启动](#增加docker开机启动)
* [更改docker存储位置](#更改docker存储位置)
* [docker启动](#docker启动)

##### 增加docker源
```
yum install -y yum-utils  
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo  
yum makecache fast
```
##### 安装docker-ce
```
yum -y install docker-ce
```
##### 增加docker开机启动
```
systemctl enable docker
```
##### 更改docker存储位置
```
mkdir /mnt/docker  
ln -s /mnt/docker /var/lib/docker
```
##### docker启动
```
systemctl start docker
```