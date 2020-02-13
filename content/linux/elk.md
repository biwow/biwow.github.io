## 下载
```
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.2.4.tar.gz
wget https://artifacts.elastic.co/downloads/kibana/kibana-6.2.4-linux-x86_64.tar.gz
wget https://artifacts.elastic.co/downloads/logstash/logstash-6.2.4.tar.gz
```
## 创建容器
```
docker run -itd --restart=unless-stopped -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone -v /data/elasticsearch:/data -privileged -p 0.0.0.0:9200:9200 -p 0.0.0.0:9300:9300 --name elasticsearch --workdir=/data -d centos
docker run -itd --restart=unless-stopped -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone -v /data/kibana:/data -p 0.0.0.0:5601:5601 --name kibana --workdir=/data -d centos
docker run -itd --restart=unless-stopped -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone -v /data/logstash:/data -p 0.0.0.0:9100:9100 --name logstash --workdir=/data -d biwow/jdk8
```
## elsearch配置

```
# 增加新用户
groupadd elsearch && /usr/sbin/useradd -g elsearch elsearch
# elasticsearch-6.2.4/config/elasticsearch.yml 
network.host: 0.0.0.0
# 9300端口： ES节点之间通讯使用；9200端口： ES节点 和 外部 通讯使用
su elsearch
bin/elasticsearch
```
> max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144] 
```
# /usr/lib/sysctl.d/50-default.conf
vm.max_map_count=655360
# sysctl -p /usr/lib/sysctl.d/50-default.conf
```
> 访问 http://192.168.48.128:9200/

## kibana配置
```
# config/kibana.yml
elasticsearch.url: "http://192.168.48.128:9200"
server.host: "0.0.0.0"
```
> 访问 http://192.168.48.128:5601