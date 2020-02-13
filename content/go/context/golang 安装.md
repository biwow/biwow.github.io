```
wget https://dl.google.com/go/go1.12.14.linux-amd64.tar.gz
tar -C /usr/local -xzf go1.12.14.linux-amd64.tar.gz

vim /etc/profile
export GOROOT=/usr/local/go
export PATH=$PATH:$GOROOT/bin
export GOPATH=/mnt/golang
source /etc/profile
```
