```
#!/bin/bash
#The docker install script

#如果任何语句的执行结果不是true则应该退出
set -e

echo "docker 服务安装中，请您稍等！"
#安装yum工具包
yum install -y yum-utils >/dev/null 2>&1

#下载docker软件包
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo >/dev/null 2>&1

#建立yun缓存
yum makecache fast >/dev/null 2>&1

#安装docker
yum -y install docker-ce >/dev/null 2>&1

#启动docker
systemctl start docker

#设置开机自启动docker服务
systemctl enable docker >/dev/null 2>&1

#查看docker版本
echo ""
echo "#################查看docker版本#####################"
docker version

sleep 3
echo ""
#查看docker进程
echo "################查看docker进程#####################"
ps -elf |grep docker

echo ""
echo "docker 服务已安装完成，请放心使用！！！"

```