## docker compose部署服务
> https://github.com/docker/compose 下载最新版本
```
#下载compose脚本
curl -L https://github.com/docker/compose/releases/download/1.19.0-rc2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
#给脚本设置可执行权限
chmod +x /usr/local/bin/docker-compose  
#查看版本
docker-compose version
#启动整个应用
docker-compose up -d
#查看信息
docker-compose ps
#停止整个应用
docker-compose stop
#对容器执行命令
docker-compose run web env
#停止并删除容器
docker-compose down --volumes --rmi all
#进入到指定容器
docker-compose exec web sh
#显示日志
docker-compose logs -f --tail=200 
docker-compose logs -f mimosa  
#重启容器
docker-compose restart -t=1 web
#设置服务的个数
docker-compose scale web=2 worker=3
```
vi docker-compose.yml
```
version: '3'
services:
  openresty:
    image: biwow/openresty:1.9
    container_name: Aopenresty
    volumes:
      - "./openresty/nginx/conf:/usr/local/openresty/nginx/conf"
      - "./openresty/nginx/logs:/usr/local/openresty/nginx/logs"
      - "./openresty/nginx/html:/usr/local/openresty/nginx/html"
      - "./openresty/nginx/upload_temp:/usr/local/openresty/nginx/upload_temp"
      - "/etc/localtime:/etc/localtime"
      - "/etc/timezone:/etc/timezone"
    ports:
      - "10080:80"
      - "10443:443"
    extra_hosts:
      - "vip.gh.com:192.168.1.142"
    restart: unless-stopped
  mimosa:
    build: ./java
    container_name: Amimosa
    volumes:
      - "./mimosa:/data"
      - "/etc/localtime:/etc/localtime"
      - "/etc/timezone:/etc/timezone"
    ports:
      - "18899:8899"
    extra_hosts:
      - "vip.gh.com:192.168.1.142"
    restart: unless-stopped
  settlement:
    build: ./java
    container_name: Asettlement
    volumes:
      - "./settlement:/data"
      - "/etc/localtime:/etc/localtime"
      - "/etc/timezone:/etc/timezone"
    ports:
      - "18883:8883"
    extra_hosts:
      - "vip.gh.com:192.168.1.142"
    restart: unless-stopped
  cms:
    build: ./java
    container_name: Acms
    volumes:
      - "./cms:/data"
      - "/etc/localtime:/etc/localtime"
      - "/etc/timezone:/etc/timezone"
    ports:
      - "17082:7082"
    extra_hosts:
      - "vip.gh.com:192.168.1.142"
    restart: unless-stopped
  operate:
    build: ./java
    container_name: Aoperate
    volumes:
      - "./operate:/data"
      - "/etc/localtime:/etc/localtime"
      - "/etc/timezone:/etc/timezone"
    ports:
      - "18832:8832"
    extra_hosts:
      - "vip.gh.com:192.168.1.142"
    restart: unless-stopped
  mysql:
    image: mysql:5.6
    container_name: Amysql
    volumes:
      - "./mysql/data:/data"
      - "./mysql/my.cnf:/etc/mysql/my.cnf"
      - "/etc/localtime:/etc/localtime"
      - "/etc/timezone:/etc/timezone"
    environment:
      - MYSQL_ROOT_PASSWORD=123456
    ports:
      - "13306:3306"
    extra_hosts:
      - "vip.gh.com:192.168.1.142"
    restart: unless-stopped
  redis:
    build: ./redis
    container_name: Aredis
    volumes:
      - "/etc/localtime:/etc/localtime"
      - "/etc/timezone:/etc/timezone"
    ports:
      - "16379:6379"
    extra_hosts:
      - "vip.gh.com:192.168.1.142"
    restart: unless-stopped
```