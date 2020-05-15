## 安装依赖工具
### jdk1.8安装
打开 https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html  ，点击下载对应的RPM版本。运行下面命令进行安装。
```
rpm -ivh jdk-8u221-linux-x64.rpm
```

### nginx安装

```
yum -y install gcc-c++ zlib-devel openssl--devel pcre-devel // nginx依赖包  
wget http://nginx.org/download/nginx-1.16.1.tar.gz          // 下载nginx最新版本
tar zxvf nginx-1.16.1.tar.gz
cd nginx-1.16.1
./configure  // 配置nginx，采用默认配置
make && make install
```
### sbt安装
```
curl https://bintray.com/sbt/rpm/rpm > bintray-sbt-rpm.repo
mv bintray-sbt-rpm.repo /etc/yum.repos.d/
yum install sbt -y
```

### protobuf安装

```
wget https://github.com/protocolbuffers/protobuf/releases/download/v3.9.1/protoc-3.9.1-linux-x86_64.zip
unzip protoc-3.9.1-linux-x86_64.zip "bin/protoc" -d /root/
mv /root/bin/protoc /usr/bin/
```

## 编译
```
tar zxvf PBE.tar.gz
cd /root/PBE/rootcontroller
sbt //下载依赖包
sbt:rootcontroller> stage  //编译项目为可执行文件
```
- libatomic.so.1: cannot open shared object file 的解决办法  
从别处拷贝到libatomic.so.1文件到/usr/lib64里面，然后再次stage

```
cd /root/PBE/rootcontroller/target/universal/stage/bin

```
