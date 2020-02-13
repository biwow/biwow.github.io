[TOC]
# linux安装maven
```
wget http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz  
tar zxvf apache-maven-3.3.9-bin.tar.gz  
mv apache-maven-3.3.9 /usr/local/maven  
#vi /etc/profile
M2_HOME=/usr/local/maven
export PATH=${M2_HOME}/bin:${PATH}
source /etc/profile
mvn -v
```
