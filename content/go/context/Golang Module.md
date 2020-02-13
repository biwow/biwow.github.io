 - 在Golang1.11版本中需要使用export GO111MODULE=on来显式开启go module
 - 在Golang1.12之后默认开启了module
 - 使用module之前必须安装git

### 初始化一个module
```
go mod init github.com/seaio-co/sea
```
### 将项目的依赖包拷贝到项目的vendor目录中
在使用了go mod之后，项目依赖的全部依赖包都会在$GOPATH/pkg/mod/cache/download/
```
go mod vendor
```