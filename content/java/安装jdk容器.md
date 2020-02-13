## 资源下载
百度网盘下载地址： 链接：https://pan.baidu.com/s/1MqPq4KQeizSUMqf6MdurZg 密码：3q9r

## 第一步：导入镜像
从云盘中下载jdk8.tar镜像文件，把镜像导入到部署服务器
```
docker load <jdk8.tar
```

## 第二步：准备项目文件
1. 在服务器下创建项目文件夹  

```
mkdir -p /data/project
```
2. 拷贝云盘中的start.sh到项目文件夹根目录，并修改为可执行权限  

```
chmod +x start.sh
```
3. 拷贝项目jar包到项目文件夹根目录

## 第三步 进入项目文件夹根目录，生成容器
```
docker run -itd --restart=unless-stopped -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone -v $(pwd):/data -p 8080:8080 ph/jdk8
```
