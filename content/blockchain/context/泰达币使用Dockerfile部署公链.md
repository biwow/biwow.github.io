# 1、下载基础镜像
> docker pull buildpack-deps:jessie-curl

# 2、编写Dockerfile
> [root@localhost]# vim Dockerfile 

```
FROM buildpack-deps:jessie-curl
RUN wget -O omnicore.tar.gz https://github.com/OmniLayer/omnicore/releases/download/v0.3.1/omnicore-0.3.1-x86_64-linux-gnu.tar.gz \
        && tar -xzvf omnicore.tar.gz \
        && cd omnicore-0.3.1//bin \
        && mv bitcoin-tx omnicore-cli omnicored omnicore-qt  /usr/local/bin
EXPOSE 8333 8332
WORKDIR /root/.bitcoin
ENTRYPOINT ["omnicored"]
CMD ["-conf=/root/.bitcoin/bitcoin.conf"]

```

# 3、准备需要映射给容器的目录及文件
> [root@localhost]# mkdir data

> [root@localhost]# vim bitcoin.conf

```
server=1
rpcuser=admin
rpcpassword=mL5HoOV34k1r
rpcport=8332
txindex=1
datacarriersize=80
logtimestamps=1
omnidebug=tally
omnidebug=packets
omnidebug=pending
```
#### 参数解释
```
rpcuser=用户名    JSON-RPC 连接使用的用户名
rpcpassword=密码    JSON-RPC 连接使用的密码
txindex=1           表示对所有的交易进行索引；否则默认只对与钱包地址有关的交易索引 


datacarriersize=80    嵌入在OP_RETURN脚本中的有效载荷的最大字节大小，可不写
logtimestamps=1       可不写
omnidebug=tally
omnidebug=packets   
omnidebug=pending     启用或禁用日志类别，可以"all"，"none"，可不写
```

# 4、build泰达币核心镜像
> docker build . -t btc/omnicore:0.3.1


```
[root@localhost /]# docker images
REPOSITORY           TAG                            IMAGE ID            CREATED             SIZE
btc/omnicore       0.3.1                          25d452d6269b        About an hour ago   259MB
```

# 5、启动泰达币核心容器

```
docker run -itd --restart=unless-stopped -v /etc/localtime:/etc/localtime -v /etc/timezone:/etc/timezone --name omnicored -v $(pwd)/data:/root/.bitcoin -v $(pwd)/bitcoin.conf:/root/.bitcoin/bitcoin.conf -p 8332:8332 -p 8333:8333 btc/omnicore:0.3.1
```


# 6、查看日志

```
[root@localhost data]# tail  -f /root/data/debug.log 
4e43ea770a7ee470e40 height=154912 version=0x00000001 log2_work=67.242901 tx=1923159 date='2011-11-27 00:24:18' progress=0.003446 cache=161.8MiB(620253tx)
2019-01-12 09:19:28 UpdateTip: new best=00000000000001ba5b24650750883bf31ae32b1994a3b5d3e65c6ad56f65e395 height=154913 version=0x00000001 log2_work=67.242943 tx=1923174 date='2011-11-27 00:27:46' progress=0.003446 cache=161.8MiB(620258tx)
2019-01-12 09:19:28 UpdateTip: new best=0000000000000dc03672ac02825b5e596df9778e112ae3ac16d3ce9f7656d0c9 height=154914 version=0x00000001 log2_work=67.242985 tx=1923202 date='2011-11-27 00:38:26' progress=0.003446 cache=161.8MiB(620268tx)
2019-01-12 09:19:28 UpdateTip: new best=00000000000001a5d6371ac7cf2dd1acfb2592ebc735c954d580910292540011 height=154915 version=0x00000001 log2_work=67.243028 tx=1923225 date='2011-11-27 00:52:19' progress=0.003446 cache=161.8MiB(620274tx)
2019-01-12 09:19:28 UpdateTip: new best=00000000000006ac50d4829167edb9cab04572ab0ac3248997b4867a5de966b9 height=154916 version=0x00000001 log2_work=67.24307 tx=1923236 date='2011-11-27 00:53:27' progress=0.003446 cache=161.8MiB(620279tx)
2019-01-12 09:19:28 UpdateTip: new best=0000000000000ba7d4bc4e05b3d717ff225cf8946dd56eb3b41464509707cfef height=154917 version=0x00000001 log2_work=67.243112 tx=1923250 date='2011-11-27 00:55:38' progress=0.003446 cache=161.9MiB(620289tx)
2019-01-12 09:19:28 UpdateTip: new best=0000000000000d87584adf63fbbb21a2563bbc0d79eec24f88808fb1a0a35e68 height=154918 version=0x00000001 log2_work=67.243155 tx=1923334 date='2011-11-27 01:20:51' progress=0.003446 cache=161.9MiB(620342tx)
2019-01-12 09:19:28 UpdateTip: new best=00000000000000d67c93180bfb28073f3d94e7a259f3dc9e3abeaefdbd6561f1 height=154919 version=0x00000001 log2_work=67.243197 tx=1923454 date='2011-11-27 01:24:17' progress=0.003447 cache=161.9MiB(620456tx)
2019-01-12 09:19:28 UpdateTip: new best=000000000000086718a39d9b170fcf64a62df1c539610c63caf326d3c8d1299b height=154920 version=0x00000001 log2_work=67.243239 tx=1923475 date='2011-11-27 01:28:23' progress=0.003447 cache=161.9MiB(620468tx)
2019-01-12 09:19:28 UpdateTip: new best=00000000000008cb1f2924d921b8ce77323e2b900295d43f2d9d1898e3792b03 height=154921 version=0x00000001 log2_work=67.243281 tx=1923486 date='2011-11-27 01:30:24' progress=0.003447 cache=161.9MiB(620476tx)
2019-01-12 09:19:28 UpdateTip: new best=0000000000000e0711a0217528b50a5a24b53f128bff875dc9ed410aa59c3b98 height=154922 version=0x00000001 log2_work=67.243324 tx=1923508 date='2011-11-27 01:37:59' progress=0.003447 cache=161.9MiB(620475tx)
2019-01-12 09:19:28 UpdateTip: new best=00000000000001133f9a4d65c84696712ca36fdb0f361654403082cf674e0294 height=154923 version=0x00000001 log2_work=67.243366 tx=1923569 date='2011-11-27 02:23:45' progress=0.003447 cache=161.9MiB(620485tx)
2019-01-12 09:19:28 UpdateTip: new best=00000000000006e748dd5faa421eed348990cc31f0ec64a052374629de8a5b0c height=154924 version=0x00000001 log2_work=67.243408 tx=1923617 date='2011-11-27 02:29:07' progress=0.003447 cache=161.9MiB(620506tx)
2019-01-12 09:19:28 UpdateTip: new best=000000000000095e73b5204b933c76d76b3b7cee8170e597ba789d91d9ff4582 height=154925 version=0x00000001 log2_work=67.243451 tx=1923633 date='2011-11-27 02:36:39' progress=0.003447 cache=161.9MiB(620516tx)
2019-01-12 09:19:28 UpdateTip: new best=0000000000000564f4e024706969f7330258fa66e9a2119fb64d7efb49e0e74b height=154926 version=0x00000001 log2_work=67.243493 tx=1923652 date='2011-11-27 02:41:37' progress=0.003447 cache=161.9MiB(620521tx)
2019-01-12 09:19:28 UpdateTip: new best=00000000000008ea350020b9c30e1e8202affa49228a8042e66e0f61f7325d64 height=154927 version=0x00000001 log2_work=67.243535 tx=1923683 date='2011-11-27 02:47:49' progress=0.003447 cache=161.9MiB(620548tx)

```
