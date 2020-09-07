# 优雅退出方法一

```
package main

import (
	"fmt"
	"net/http"
	"os"
	"os/signal"
	"syscall"
	"time"
)

var status = true

// 优雅退出go守护进程
func main()  {
	//创建监听退出chan
	c := make(chan os.Signal)
	//监听指定信号 ctrl+c kill
	signal.Notify(c, syscall.SIGHUP, syscall.SIGINT, syscall.SIGTERM, syscall.SIGQUIT)
	go func() {
		for s := range c {
			switch s {
			case syscall.SIGHUP, syscall.SIGINT, syscall.SIGTERM, syscall.SIGQUIT:
				fmt.Println("退出", s)
				ExitFunc()
			default:
				fmt.Println("other", s)
			}
		}
	}()

	fmt.Println("进程启动...")
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		if status {
			w.Write([]byte("Hello, World!"))
		} else {
			w.Write([]byte("stop!"))
		}

	})
	http.ListenAndServe(":8080", nil)
}

func ExitFunc()  {
	fmt.Println("开始退出...")
	fmt.Println("执行清理...")
	fmt.Println("结束退出...")
	status = false
	go stop()

}

func stop() {
	fmt.Println("stop 5...")
	time.Sleep(time.Duration(5) * time.Second)
	fmt.Println("stop ...")
	//os.Exit(0)
}
```

# 优雅退出方法二

```
package main

import (
	"fmt"
	"os"
	"os/signal"
	"time"
)

var status = true

func main() {
	fmt.Println("开始")

	go func() {
		var sigc = make(chan os.Signal, 1)
		signal.Notify(sigc, os.Interrupt, os.Kill)
		<-sigc
		fmt.Println("Got interrupt, shutting down...")
		go stop()
	}()

	<-make(chan struct{})

}

func stop() {
	fmt.Println("stop 5...")
	time.Sleep(time.Duration(5) * time.Second)
	fmt.Println("stop ...")
	os.Exit(0)
}
```