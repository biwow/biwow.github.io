#### 一次性生效
```
swapoff -a && swapon -a  
可以执行命令刷新一次SWAP（将SWAP里的数据转储回内存，并清空SWAP里的数据）
```
#### 永久生效
```
echo "vm.swappiness = 0">> /etc/sysctl.conf  
sysctl -p
```