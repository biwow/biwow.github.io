### 下载代码
```
git clone -b v0.3.0 https://github.com/OmniLayer/omnicore.git
```
### 安装依赖
```
yum update
yum install -y autoconf automake libtool gcc build-essential gcc-c++ make autoconfig boost-devel openssl-devel libevent-devel
# 安装Berkeley DB
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/l/libdb4-4.8.30-13.el7.x86_64.rpm
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/l/libdb4-devel-4.8.30-13.el7.x86_64.rpm
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/l/libdb4-cxx-4.8.30-13.el7.x86_64.rpm
wget http://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/l/libdb4-cxx-devel-4.8.30-13.el7.x86_64.rpm
rpm -ivh libdb4-4.8.30-13.el7.x86_64.rpm
rpm -ivh libdb4-devel-4.8.30-13.el7.x86_64.rpm
rpm -ivh libdb4-cxx-4.8.30-13.el7.x86_64.rpm
rpm -ivh libdb4-cxx-devel-4.8.30-13.el7.x86_64.rpm
```
### 编译
```
cd omnicore/
./autogen.sh
./configure
make
```