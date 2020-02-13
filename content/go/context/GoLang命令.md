[TOC]
# 查看可用命令
直接在终端中输入 go help 即可显示所有的 go 命令以及相应命令功能简介，主要有下面这些:  

* build: 编译包和依赖
* clean: 移除对象文件
* doc: 显示包或者符号的文档
* env: 打印go的环境信息
* bug: 启动错误报告
* fix: 运行go tool fix
* fmt: 运行gofmt进行格式化
* generate: 从processing source生成go文件
* get: 下载并安装包和依赖
* install: 编译并安装包和依赖
* list: 列出包
* run: 编译并运行go程序
* test: 运行测试
* tool: 运行go提供的工具
* version: 显示go的版本
* vet: 运行go tool vet  

命令的使用方式为: `go command [args]`, 除此之外，可以使用`go help <command>` 来显示指定命令的更多帮助信息。

在运行 go help 时，不仅仅打印了这些命令的基本信息，还给出了一些概念的帮助信息:  
* c: Go和c的相互调用
* buildmode: 构建模式的描述
* filetype: 文件类型
* gopath: GOPATH环境变量
* environment: 环境变量
* importpath: 导入路径语法
* packages: 包列表的描述
* testflag: 测试符号描述
* testfunc: 测试函数描述  

同样使用 `go help <topic>`来查看这些概念的的信息。

# build 和 run 命令  

就像其他静态类型语言一样，要执行 go 程序,需要先编译，然后在执行产生的可执行文件。`go build` 命令就是用来编译 go程序生成可执行文件的。但并不是所有的 go 程序都可以编译生成可执行文件的, 要生成可执行文件，go程序需要满足两个条件:

* 该go程序需要属于main包
* 在main包中必须还得包含main函数  

也就是说go程序的入口就是 `main.main`, 即main包下的main函数,　例子(hello.go):

```
package main

import "fmt"

func main() {
    fmt.Println("Hello World!")
}
```
编译hello.go,然后运行可执行程序:  

```
$ go run hello.go   # 将会生成可执行文件 hello
$ ./hello           # 运行可执行文件
Hello World!
```
go build+文件列表:  

```
go build file1.go file2.go……
```
可编译同目录的多个源码文件，go build 会编译这些源码，输出可执行文件  

### go build编译时的附加参数  

go build 还有一些附加参数，可以显示更多的编译信息和更多的操作，详见下表所示。

附加参数 | 备  注
:---:|---
-v | 编译时显示包名
-p n | 开启并发编译，默认情况下该值为 CPU 逻辑核数
-a | 强制重新构建
-n | 打印编译时会用到的所有命令，但不真正执行
-x | 打印编译时会用到的所有命令
-race | 开启竞态检测



上面就是 go build 的基本用法，另外如果使用 go build 编译的不是一个可执行程序，而是一个包，那么将不会生成可执行文件。

而 `go run` 命令可以将上面两步并为一步执行(不会产生中间文件)。

```
$ go run hello.go
Hello World!
```

注意：`go run` 不会在运行目录下生成任何文件，可执行文件被放在临时文件中被执行，工作目录被设置为当前目录。在 go run 的后部可以添加参数，这部分参数会作为代码可以接受的命令行输入提供给程序。

go run 不能使用“go run+包”的方式进行编译，如需快速编译运行包，需要使用如下步骤来代替：  
* 使用 go build 生成可执行文件。
* 运行可执行文件。

# clent命令

这个命令是用来移除当前源码包和关联源码包里面编译生成的文件。这些文件包括

```
_obj/            旧的object目录，由Makefiles遗留
_test/           旧的test目录，由Makefiles遗留
_testmain.go     旧的gotest文件，由Makefiles遗留
test.out         旧的test记录，由Makefiles遗留
build.out        旧的test记录，由Makefiles遗留
*.[568ao]        object文件，由Makefiles遗留

DIR(.exe)        由go build产生
DIR.test(.exe)   由go test -c产生
MAINFILE(.exe)   由go build MAINFILE.go产生
*.so             由 SWIG 产生
```
我一般都是利用这个命令清除编译文件，然后github递交源码，在本机测试的时候这些编译文件都是和系统相关的，但是对于源码管理来说没必要。
```
$ go clean -i -n
cd /Users/astaxie/develop/gopath/src/mathapp
rm -f mathapp mathapp.exe mathapp.test mathapp.test.exe app app.exe
rm -f /Users/astaxie/develop/gopath/bin/mathapp
```

附加参数 | 备注
:---:|---
 -i | 清除关联的安装的包和可运行文件，也就是通过go install安装的文件
 -n |  把需要执行的清除命令打印出来，但是不执行，这样就可以很容易的知道底层是如何运行的
 -r |  循环的清除在import中引入的包
 -x |  打印出来执行的详细命令，其实就是-n打印的执行版本


# fmt 和 doc 命令  
go 语言有一个褒贬不一的特性，就是对格式的要求很严格，我是很喜欢这个特性的，因为可以保持代码的清晰一致，编译组合开发，并且go还提供了一个非常强大的工具来格式化代码，它就是 `go fmt sourcefile.go`, 不过通常其实不需要我们手动调用，各种编辑器都可以帮助我们自动完成格式化。

`go doc` 命令可以方便我们快速查看包文档，`go doc package` 命令将会在终端中打印出指定 package 的文档。

另外有一个与 `go doc` 命令相关的命令是 `godoc`, 可以通过它启动我们自己的文档服务器:  

```
godoc -http=:8080
```
然后我们就可与在浏览器`localhost:8080`中查看go文档了

# get 命令

go get 可以借助代码管理工具通过远程拉取或更新代码包及其依赖包，并自动完成编译和安装。整个过程就像安装一个 App 一样简单。  


使用 go get 前，需要安装与远程包匹配的代码管理工具，如 Git、SVN、HG 等，参数中需要提供一个包名。

## 远程包的路径格式  

Go 语言的代码被托管于 Github.com 网站，该网站是基于 Git 代码管理工具的，很多有名的项目都在该网站托管代码。其他类似的托管网站还有 code.google.com、bitbucket.org 等。

这些网站的项目包路径都有一个共同的标准，参见下图所示  

![image](c.biancheng.net/uploads/allimg/180820/1-1PR0110433A4.jpg)

图中的远程包路径是 Go 语言的源码，这个路径共由 3 个部分组成：
* 网站域名：表示代码托管的网站，类似于电子邮件 @ 后面的服务器地址。
* 作者或机构：表明这个项目的归属，一般为网站的用户名，如果需要找到这个作者下的所有项目，可以直接在网站上通过搜索“域名/作者”进行查看。这部分类似于电子邮件 @ 前面的部分。
* 项目名：每个网站下的作者或机构可能会同时拥有很多的项目，图中标示的部分表示项目名称。

## go get+远程包

默认情况下，go get 可以直接使用。例如，想获取 go 的源码并编译，使用下面的命令行即可：

```
$ go get github.com/davyxu/cellnet
```
获取前，请确保 GOPATH 已经设置。Go 1.8 版本之后，GOPATH 默认在用户目录的 go 文件夹下。

cellnet 只是一个网络库，并没有可执行文件，因此在 go get 操作成功后 GOPATH 下的 bin 目录下不会有任何编译好的二进制文件。

需要测试获取并编译二进制的，可以尝试下面的这个命令。当获取完成后，就会自动在 GOPATH 的 bin 目录下生成编译好的二进制文件。


```
$ go get github.com/davyxu/tabtoy
```

## go get使用时的附加参数
使用 go get 时可以配合附加参数显示更多的信息及实现特殊的下载和安装操作，详见下表所示。


附加参数 | 附加参数
:---: |---
-v | 显示操作流程的日志及信息，方便检查错误
-u | 下载丢失的包，但不会更新已经存在的包
-d | 只下载，不安装
-insecure | 允许使用不安全的 HTTP 方式进行下载操作

# install 命令  
go install 的功能和 go build 类似，附加参数绝大多数都可以与 go build 通用。go install 只是将编译的中间文件放在 GOPATH 的 pkg 目录下，以及固定地将编译结果放在 GOPATH 的 bin 目录下。


go install 的编译过程有如下规律：
* go install 是建立在 GOPATH 上的，无法在独立的目录里使用 go install。
* GOPATH 下的 bin 目录放置的是使用 go install 生成的可执行文件，可执行文件的名称来自于编译时的包名。
* go install 输出目录始终为 GOPATH 下的 bin 目录，无法使用-o附加参数进行自定义。
* GOPATH 下的 pkg 目录放置的是编译期间的中间文件。

# test命令

Go 语言拥有一套单元测试和性能测试系统，仅需要添加很少的代码就可以快速测试一段需求代码。

性能测试系统可以给出代码的性能数据，帮助测试者分析性能问题。

**提示**  


单元测试（unit testing），是指对软件中的最小可测试单元进行检查和验证。对于单元测试中单元的含义，一般要根据实际情况去判定其具体含义，如C语言中单元指一个函数，Java 里单元指一个类，图形化的软件中可以指一个窗口或一个菜单等。总的来说，单元就是人为规定的最小的被测功能模块。

单元测试是在软件开发过程中要进行的最低级别的测试活动，软件的独立单元将在与程序的其他部分相隔离的情况下进行测试。

## 单元测试——测试和验证代码的框架

要开始一个单元测试，需要准备一个 go 源码文件，在命名文件时需要让文件必须以`_test`结尾。

单元测试源码文件可以由多个测试用例组成，每个测试用例函数需要以Test为前缀，例如：

```
func TestXXX( t *testing.T )
```
* 测试用例文件不会参与正常源码编译，不会被包含到可执行文件中。
* 测试用例文件使用 go test 指令来执行，没有也不需要 main() 作为函数入口。所有在以_test结尾的源码内以Test开头的函数会自动被执行。
* 测试用例可以不传入 *testing.T 参数。


```
package code11_3
import "testing"
func TestHelloWorld(t *testing.T) {
    t.Log("hello world")
}
```
代码说明如下：
* 第 5 行，单元测试文件 (*_test.go) 里的测试入口必须以 Test 开始，参数为 *testing.T 的函数。一个单元测试文件可以有多个测试入口。
* 第 6 行，使用 testing 包的 T 结构提供的 Log() 方法打印字符串。

### 1) 单元测试命令行
单元测试使用 go test 命令启动，例如：  

```
$ go test helloworld_test.go
ok          command-line-arguments        0.003s
$ go test -v helloworld_test.go
=== RUN   TestHelloWorld
--- PASS: TestHelloWorld (0.00s)
        helloworld_test.go:8: hello world
PASS
ok          command-line-arguments        0.004s
```
代码说明如下：
* 第 1 行，在 go test 后跟 helloworld_test.go 文件，表示测试这个文件里的所有测试用例。
* 第 2 行，显示测试结果，ok 表示测试通过，command-line-arguments 是测试用例需要用到的一个包名，0.003s 表示测试花费的时间。
* 第 3 行，显示在附加参数中添加了-v，可以让测试时显示详细的流程。
* 第 4 行，表示开始运行名叫 TestHelloWorld 的测试用例。
* 第 5 行，表示已经运行完 TestHelloWorld 的测试用例，PASS 表示测试成功。
* 第 6 行打印字符串 hello world。

### 2) 运行指定单元测试用例  
go test 指定文件时默认执行文件内的所有测试用例。可以使用`-run`参数选择需要的测试用例单独执行，参考下面的代码。

```
package code11_3
import "testing"
func TestA(t *testing.T) {
    t.Log("A")
}
func TestAK(t *testing.T) {
    t.Log("AK")
}
func TestB(t *testing.T) {
    t.Log("B")
}
func TestC(t *testing.T) {
    t.Log("C")
}
```
这里指定 TestA 进行测试：  

```
$ go test -v -run TestA select_test.go
=== RUN   TestA
--- PASS: TestA (0.00s)
        select_test.go:6: A
=== RUN   TestAK
--- PASS: TestAK (0.00s)
        select_test.go:10: AK
PASS
ok          command-line-arguments        0.003s
```
TestA 和 TestAK 的测试用例都被执行，原因是-run跟随的测试用例的名称支持正则表达式，使用-run TestA$即可只执行 TestA 测试用例。
### 3) 标记单元测试结果
当需要终止当前测试用例时，可以使用 FailNow，参考下面的代码。

```
func TestFailNow(t *testing.T) {
    t.FailNow()
}
```
还有一种只标记错误不终止测试的方法，代码如下：

```
func TestFail(t *testing.T) {
    fmt.Println("before fail")
    t.Fail()
    fmt.Println("after fail")
}
```
测试结果如下：

```
=== RUN   TestFail
before fail
after fail
--- FAIL: TestFail (0.00s)
FAIL
exit status 1
FAIL        command-line-arguments        0.002s
```
从日志中看出，第 5 行调用 Fail() 后测试结果标记为失败，但是第 7 行依然被程序执行了。

### 4) 单元测试日志
每个测试用例可能并发执行，使用 testing.T 提供的日志输出可以保证日志跟随这个测试上下文一起打印输出。testing.T 提供了几种日志输出方法，详见下表所示。  

单元测试框架提供的日志方法
方  法 | 	备  注
---|---
Log	| 打印日志，同时结束测试
Logf	| 	格式化打印日志，同时结束测试
Error	| 	打印错误日志，同时结束测试
Errorf	| 	格式化打印错误日志，同时结束测试
Fatal	| 	打印致命日志，同时结束测试
Fatalf	| 	格式化打印致命日志，同时结束测试

开发者可以根据实际需要选择合适的日志。  

## 基准测试——获得代码内存占用和运行效率的性能数据  
基准测试可以测试一段程序的运行性能及耗费 CPU 的程度。Go 语言中提供了基准测试框架，使用方法类似于单元测试，使用者无须准备高精度的计时器和各种分析工具，基准测试本身即可以打印出非常标准的测试报告。

### 1) 基础测试基本使用

下面通过一个例子来了解基准测试的基本使用方法。

```
package code11_3
import "testing"
func Benchmark_Add(b *testing.B) {
    var n int
    for i := 0; i < b.N; i++ {
        n++
    }
}
```

这段代码使用基准测试框架测试加法性能。第 7 行中的 b.N 由基准测试框架提供。测试代码需要保证函数可重入性及无状态，也就是说，测试代码不使用全局变量等带有记忆性质的数据结构。避免多次运行同一段代码时的环境不一致，不能假设 N 值范围。

使用如下命令行开启基准测试：


```
$ go test -v -bench=. benchmark_test.go
goos: linux
goarch: amd64
Benchmark_Add-4           20000000         0.33 ns/op
PASS
ok          command-line-arguments        0.700s
```
代码说明如下：
* 第 1 行的`-bench=.`表示运行 benchmark_test.go 文件里的所有基准测试，和单元测试中的-run类似。
* 第 4 行中显示基准测试名称，2000000000 表示测试的次数，也就是 testing.B 结构中提供给程序使用的 N。“0.33 ns/op”表示每一个操作耗费多少时间（纳秒）。

注意：Windows 下使用 go test 命令行时，`-bench=.`应写为`-bench="."`。 

### 2) 基准测试原理
基准测试框架对一个测试用例的默认测试时间是 1 秒。开始测试时，当以 Benchmark 开头的基准测试用例函数返回时还不到 1 秒，那么 testing.B 中的 N 值将按 1、2、5、10、20、50……递增，同时以递增后的值重新调用基准测试用例函数。  

### 3) 自定义测试时间
通过`-benchtime`参数可以自定义测试时间，例如：

```
$ go test -v -bench=. -benchtime=5s benchmark_test.go
goos: linux
goarch: amd64
Benchmark_Add-4           10000000000                 0.33 ns/op
PASS
ok          command-line-arguments        3.380s
```

### 4) 测试内存
基准测试可以对一段代码可能存在的内存分配进行统计，下面是一段使用字符串格式化的函数，内部会进行一些分配操作。


```
func Benchmark_Alloc(b *testing.B) {
    for i := 0; i < b.N; i++ {
        fmt.Sprintf("%d", i)
    }
}
```

在命令行中添加`-benchmem`参数以显示内存分配情况，参见下面的指令：

```
$ go test -v -bench=Alloc -benchmem benchmark_test.go
goos: linux
goarch: amd64
Benchmark_Alloc-4 20000000 109 ns/op 16 B/op 2 allocs/op
PASS
ok          command-line-arguments        2.311s
```
代码说明如下：  
* 第 1 行的代码中-bench后添加了 Alloc，指定只测试 Benchmark_Alloc() 函数。
* 第 4 行代码的“16 B/op”表示每一次调用需要分配 16 个字节，“2 allocs/op”表示每一次调用有两次分配。

开发者根据这些信息可以迅速找到可能的分配点，进行优化和调整

### 5) 控制计时器

有些测试需要一定的启动和初始化时间，如果从 Benchmark() 函数开始计时会很大程度上影响测试结果的精准性。testing.B 提供了一系列的方法可以方便地控制计时器，从而让计时器只在需要的区间进行测试。我们通过下面的代码来了解计时器的控制。


```
func Benchmark_Add_TimerControl(b *testing.B) {
    // 重置计时器
    b.ResetTimer()
    // 停止计时器
    b.StopTimer()
    // 开始计时器
    b.StartTimer()
    var n int
    for i := 0; i < b.N; i++ {
        n++
    }
}
```
从 Benchmark() 函数开始，Timer 就开始计数。StopTimer() 可以停止这个计数过程，做一些耗时的操作，通过 StartTimer() 重新开始计时。ResetTimer() 可以重置计数器的数据。

计数器内部不仅包含耗时数据，还包括内存分配的数据。

## test命令小总结

```

go test package                                 //生成并运行测试该源码包下面所有_test文件下所有测试方法直到测试完毕

go test *_test.go                               //生成并运行测试该文件下所有测试方法直到测试完毕

go test -v *_test.go                            //测试该文件，并显示测试的详细命令

go test -v -bench=. *_test.go                   //执行相应的benchmarks方法，例如 -bench=.执行所有   

go test -cover *_test.go                        //开启测试覆盖率

go test -run regexp *_test.go                   //正则匹配，例如 -run=Array 那么就执行包含有Array开头的函数  

go test -v -run Test_A *_test.go                //自定义测试方法

go test -v -bench=. -benchtime=5s *_test.go     //自定义测试时间

go test -v -bench=Alloc -benchmem b*_test.go    //测试内存，本例为对指定方法进行测试并测试内存

go test -cpuprofile cpu.out *_test.go           //输出cpu性能分析文件

go test -memprofile mem.out *_test.go           //输出内存性能分析文件 

go test -blockprofile block.out  *_test.go      //输出内部goroutine阻塞的性能分析文件 
```
# pprof命令
Go 语言工具链中的 go pprof 可以帮助开发者快速分析及定位各种性能问题，如 CPU 消耗、内存分配及阻塞分析。

性能分析首先需要使用 runtime.pprof 包嵌入到待分析程序的入口和结束处。runtime.pprof 包在运行时对程序进行每秒 100 次的采样，最少采样 1 秒。然后将生成的数据输出，让开发者写入文件或者其他媒介上进行分析。

go pprof 工具链配合 Graphviz 图形化工具可以将 runtime.pprof 包生成的数据转换为 PDF 格式，以图片的方式展示程序的性能分析结果  

## 安装第三方图形化显式分析数据工具（Graphviz）
Graphviz 是一套通过文本描述的方法生成图形的工具包。描述文本的语言叫做 DOT。

在 www.graphviz.org（http://www.graphviz.org）网站可以获取到最新的 Graphviz 各平台的安装包。

CentOS 下，可以使用 yum 指令直接安装：

```
$ yum install graphiviz
```
## 安装第三方性能分析来分析代码包

runtime.pprof 提供基础的运行时分析的驱动，但是这套接口使用起来还不是太方便，例如：
* 输出数据使用 io.Writer 接口，虽然扩展性很强，但是对于实际使用不够方便，不支持写入文件。
* 默认配置项较为复杂。

很多第三方的包在系统包 runtime.pprof 的技术上进行便利性封装，让整个测试过程更为方便。这里使用 github.com/pkg/profile 包进行例子展示，使用下面代码安装这个包：

> $ go get github.com/pkg/profile  

## 性能分析代码
下面代码故意制造了一个性能问题，同时使用 github.com/pkg/profile 包进行性能分析。

```
package main
import (
    "github.com/pkg/profile"
    "time"
)
func joinSlice() []string {
    var arr []string
    for i := 0; i < 100000; i++ {
     // 故意造成多次的切片添加(append)操作, 由于每次操作可能会有内存重新分配和移动, 性能较低
        arr = append(arr, "arr")
    }
    return arr
}
func main() {
    // 开始性能分析, 返回一个停止接口
    stopper := profile.Start(profile.CPUProfile, profile.ProfilePath("."))
    // 在main()结束时停止性能分析
    defer stopper.Stop()
    // 分析的核心逻辑
    joinSlice()
    // 让程序至少运行1秒
    time.Sleep(time.Second)
}
```
代码说明如下：
* 第 4 行，引用 github.com/pkg/profile 第三方包封装。
* 第 14 行，为了进行性能分析，这里在已知元素大小的情况下，还是使用 append() 函数不断地添加切片。性能较低，在实际中应该避免，这里为了性能分析，故意这样写。
* 第 22 行，使用 profile.Start 调用 github.com/pkg/profile 包的开启性能分析接口。这个 Start 函数的参数都是可选项，这里需要指定的分析项目是 profile.CPUProfile，也就是 CPU 耗用。profile.ProfilePath(".") 指定输出的分析文件路径，这里指定为当前文件夹。profile.Start() 函数会返回一个 Stop 接口，方便在程序结束时结束性能分析。
* 第 25 行，使用 defer，将性能分析在 main() 函数结束时停止。
* 第 28 行，开始执行分析的核心。
* 第 31 行，为了保证性能分析数据的合理性，分析的最短时间是 1 秒，使用 time.Sleep() 在程序结束前等待 1 秒。如果你的程序默认可以运行 1 秒以上，这个等待可以去掉。

性能分析需要可执行配合才能生成分析结果，因此使用命令行对程序进行编译，代码如下：

```
$ go run cpu.go
$ go tool pprof --pdf cpu.pprof > cpu.pdf
```
代码说明如下：  
第 1 行运行 cpu.go ，在当前目录输出 cpu.pprof 文件。  
第 2 行，使用 go tool 工具链输入 cpu.pprof ，生成 PDF 格式的输出文件，将输出文件重定向为 cpu.pdf 文件。这个过程中会调用 Graphviz 工具，Windows 下需将 Graphviz 的可执行目录添加到环境变量 PATH 中。

最终生成 cpu.pdf 文件，使用 PDF 查看器打开文件，观察后发现下图所示的某个地方可能存在瓶颈。  

![image](http://c.biancheng.net/uploads/allimg/180820/1-1PR0130104114.jpg)


```
func joinSlice() []string {
    const count = 100000
    var arr []string = make([]string, count)
    for i := 0; i < count; i++ {
        arr[i] = "arr"
    }
    return arr
}
```
代码说明如下：
* 第 5 行，将切片预分配 count 个数量，避免之前使用 append() 函数的多次分配。
* 第 8 行，预分配后，直接对每个元素进行直接赋值。
重新运行上面的代码进行性能分析，最终得到的 cpu.pdf 中将不会再有耗时部分。  

# 其他命令
其他命令不会经常使用，这里就不介绍了，真的用到的时候，直接使用 `go help command` 即可查看相关命令。