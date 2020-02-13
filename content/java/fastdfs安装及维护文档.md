[toc]

# 一、安装docker环境
[安装docker服务链接](http://note.youdao.com/noteshare?id=a5d8141ce5f081fe0808471d5c4e9f71&sub=08F032C2B3114A0FB4D238E3F0143F32)

# 二、部署fastdfs
##  2.1 将fastdfs项目程序包，上传到服务器中，进行解压

```
[root@localhost ~]# mkdir /opt/docker
[root@localhost ~]# cd /opt/docker/
[root@localhost docker]# ls
fastdfs-2019-06-13.zip
[root@localhost docker]# unzip fastdfs-2019-06-13.zip 

```
## 2.2 导入storage和tracker镜像

```
[root@localhost storage]# pwd
/opt/docker/fastdfs/storage
[root@localhost storage]# docker load -i storage.tar 

[root@localhost tracker]# pwd
/opt/docker/fastdfs/tracker
[root@localhost tracker]# docker load -i tracker.tar
[root@basechain-test fastdfs]# docker images
REPOSITORY           TAG                 IMAGE ID            CREATED             SIZE
biwow/storage        latest              b4a1cd3d16cd        17 months ago       231MB
biwow/tracker        latest              7e4dc27d4783        17 months ago       217MB
```
## 2.3 更改配置文件

```
[root@localhost conf]# pwd
/opt/docker/fastdfs/storage/conf

# fastdfs client组件配置文件修改
[root@localhost conf]# vim client.conf 
 14 tracker_server=172.31.56.147:22122   // tracker服务地址

# fastdfs storage组件配置文件修改
[root@localhost conf]# vim storage.conf 
118 tracker_server=172.31.56.147:22122   // tracker服务地址

[root@localhost conf]# vim mod_fastdfs.conf
 40 tracker_server=172.31.56.147:22122   // tracker服务地址


# nginx 配置文件修改
[root@localhost conf]# vim nginx.conf 
 16         server_name 172.31.56.147;     #填写服务器内网ip地址

```

##  2.4 编写fastdfs服务启动脚本

- tracker服务启动脚本
```
[root@localhost fastdfs]# pwd
/opt/docker/fastdfs

[root@localhost fastdfs]# vim tracker.sh

#!/bin/bash

docker run -itd --restart=unless-stopped --network=host -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone   --name tracker -v /opt/docker/fastdfs/tracker/conf/tracker.conf:/etc/fdfs/tracker.conf -v /opt/docker/fastdfs/tracker/tracker:/data/fastdfs/tracker biwow/tracker

docker logs -f tracker --tail 10


[root@localhost fastdfs]# chmod +x tracker.sh
```
- storage服务启动脚本

```
[root@localhost fastdfs]# pwd
/opt/docker/fastdfs

[root@localhost fastdfs]# vim storage.sh

#!/bin/bash

docker run -itd --restart=unless-stopped  --network=host   -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone --name storage -v /opt/docker/fastdfs/storage/conf:/etc/fdfs -v /opt/docker/fastdfs/storage/storage:/data/fastdfs/storage -v /opt/docker/fastdfs/storage/conf/nginx.conf:/usr/local/nginx/conf/nginx.conf biwow/storage

docker logs -f storage



[root@localhost fastdfs]# chmod +x storage.sh 
```
## 2.5. 启动fastdfs服务
**注：先启动tracker，然后启动storage（因为启动storage，会去自动连接tracker服务）**

- 启动tracker服务
```
[root@localhost fastdfs]# pwd
/opt/docker/fastdfs

[root@localhost fastdfs]# ./tracker.sh 
745205f14811eea60f89d449a301e650ee9eb4ed1d35ccfa43ba8667e78bcb37
......
```
- 启动storage服务

```
[root@localhost fastdfs]# pwd
/opt/docker/fastdfs

[root@localhost fastdfs]# ./storage.sh 
f307f47482f7b8861098a8cf1da06061c65eb96b07f28dc80c23893d2bb99a08
......
 INFO - file: tracker_client_thread.c, line: 1263, tracker server 172.31.56.147:22122, set tracker leader: 172.31.56.147:22122
```
##  2.6 测试fastdfs服务上传文件
- 上传文件测试
```
[root@localhost ~]# docker exec -it storage sh
/ # 
/ # echo "hello,word!" > test.txt
/ # /usr/bin/fdfs_upload_file /etc/fdfs/client.conf test.txt 
group1/M00/00/00/rB84k14KsEqANEcpAAAADFAsRCs734.txt

```
- 验证测试

```
[root@localhost ~]# curl http://47.52.112.248:8888/group1/M00/00/00/rB84k14KsEqANEcpAAAADFAsRCs734.txt
hello,word!
```


# 三、fastdfs重启策略

**注：先清除tracker缓存，再重启tracker服务，storage服务可根据需要重启**

## 3.1 清除tracker服务缓存
**注：tracker服务的缓存中存储的是storage节点信息及存储的文件链接信息，此时我们需要将缓存进行清除，然后再重启tracker服务，重新缓存相关信息。**

```
[root@localhost data]# pwd
/opt/docker/fastdfs/tracker/tracker/data
[root@localhost data]# ls
fdfs_trackerd.pid  storage_changelog.dat  storage_groups_new.dat  storage_servers_new.dat  storage_sync_timestamp.dat
[root@localhost data]# rm -f *
```
##  3.2 重启tracker服务
```
[root@localhost data]# docker restart tracker;docker logs -f tracker --tail 10
 INFO - file: tracker_relationship.c, line: 407, I am the new tracker leader 172.31.56.147:22122

```

## 3.3 重启storage服务

**注：根据需要进行重启storage服务**

```
[root@localhost ~]# docker restart storage;docker logs -f storage --tail 10
......
file: tracker_client_thread.c, line: 310, successfully connect to tracker server 172.31.56.147:22122, as a tracker client, my ip is 172.31.56.147
```



# 四、fastdfs常用命令
## 4.1 fastdfs的storage server的状态查询

```
[root@localhost ~]# docker exec -it storage sh
/ # fdfs_monitor /etc/fdfs/storage.conf
......
tracker server is 172.31.56.147:22122
......

	Storage 1:
		id = 172.31.56.147
		ip_addr = 172.31.56.147 (iZj6ch7pwqllfzfujmnmnfZ)  ACTIVE
```
**注意：storage正常状态必须是ACTIVE ！！！**

- 以下为storage服务的7种状态

```
FDFS_STORAGE_STATUS：INIT :初始化，尚未得到同步已有数据的源服务器

FDFS_STORAGE_STATUS：WAIT_SYNC :等待同步，已得到同步已有数据的源服务器

FDFS_STORAGE_STATUS：SYNCING :同步中

FDFS_STORAGE_STATUS：DELETED  :已删除，该服务器从本组中摘除

FDFS_STORAGE_STATUS：OFFLINE :离线

FDFS_STORAGE_STATUS：ONLINE :在线，尚不能提供服务

FDFS_STORAGE_STATUS：ACTIVE :在线，可以提供服务
```

## 4.2  文件常用命令

- 文件上传命令

fdfs_upload_file
```
# /usr/bin/fdfs_upload_file /etc/fdfs/client.conf 1.txt
```

- 文件下载命令：

fdfs_download_file
```
/ # /usr/bin/fdfs_download_file /etc/fdfs/client.conf group1/M00/00/00/rB84k14KtieAZ7SuAAAAAAAAAAA148.txt
/ # ls
rB84k14KtieAZ7SuAAAAAAAAAAA148.txt 
```
- 查看文件信息

fdfs_file_info
```
# /usr/bin/fdfs_file_info /etc/fdfs/client.conf group1/M00/00/00/rB84k14KsEqANEcpAAAADFAsRCs734.txt
source storage id: 0
source ip address: 172.31.56.147
file create timestamp: 2019-12-31 10:19:54
file size: 12
file crc32: 1345078315 (0x502C442B)

```

- 文件删除命令

fdfs_delete_file
```
# /usr/bin/fdfs_delete_file /etc/fdfs/client.conf group1/M00/00/00/rB84k14KsEqANEcpAAAADFAsRCs734.txt
```

# 五、常用配置
## 5.1 nginx回显地址配置
> 注：nginx回显地址配置即fastdfs中nginx的域名设置

- 设置回显地址域名
```
[root@localhost conf]# pwd
/opt/docker/fastdfs/storage/conf

[root@localhost conf]# vim nginx.conf 
 16         server_name www.fastdfs.com;   // 填写需要配置的域名
```
- 重启nginx服务生效配置
```
[root@localhost conf]# docker exec -it storage sh
/ # nginx -s reload
ngx_http_fastdfs_set pid=64

```
- 测试配置是否生效

```
[root@localhost ~]# curl http://www.fastdfs.com:8888/group1/M00/00/00/rB84k14KvDmAFwXrAAAAESpuN68115.txt
Nice to meet you

```

# 六、fastdfs常见报错

## 6.1 磁盘空间不足报错
- 报错内容：
```
storage上传文件时报错：tracker_query_storage fail, error no: 28, error info: No space left on device
```
- 报错原因：

```
tracker.conf 配置项 reserved_storage_space = 10%
fastdfs存储目录所在磁盘剩余空间不足10%
```
- 解决方法：

```
清理磁盘空间或扩容磁盘空间
```

## 6.2 上传文件扩展名报错

- 报错内容：
```
[2019-12-25 17:40:35] ERROR - file: storage_service.c, line: 4460, client ip: 10.1.1.136, file_ext_name: 187 00 is invalid!
```
- 报错原因：

```
fastdfs上传文件时，仅允许上传文件的扩展名规则为：【0-9】【a-z】【A-Z】
```
- 解决方法

```
修改文件扩展名为符合fastdfs定义的扩展名规则的名称
```






