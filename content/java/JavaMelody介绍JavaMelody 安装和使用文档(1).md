[TOC]
# JavaMelody介绍
&nbsp;&nbsp;&nbsp;&nbsp;JavaMelody用于对Java应用或者应用服务器的QA以及开发环境的监控。它并不是一个模拟请求类似JMeter的压力测试工具，而是一个衡量并且计算在应用上的操作信息的工具，也就是说，它只负责对行为进行监控，而不负责触发操作。JavaMelody基于请求统计生成模拟图表，并为我们的应用程序在QA或者开发上提供下面的帮助：
> - 1 给出平均的响应时间以及执行数
> - 2 在某些操作趋势变得严重前给出提示
> - 3 优化响应
> - 4 找出响应瓶颈的根本
> - 5 证实优化策略的效果
 
　　JDK版本要求：需要Java JDK在1.6或者1.6以上。
 
> 支持在以下应用服务器的部署以及监控：
> - servlet API在2.4以上
> - Tomcat 5.5 6 或者7
> - GlassFish v2或v3
> - JBoss 4,5,6,7
> - Jonas 4或5
> - Jetty 6或7
> - WebLogic 9,10,11
　　如果想要监控其他的服务器需要安装一些插件，详情阅读UserGuide
 
　　使用的浏览器最好是 Firefox Chrome或IE9
# JavaMelody安装
 
　　安装测试JavaMelody需要一个web应用，一个javaMelody的war包，以及两个jar包。
    为了紧跟潮流，我们一律采用最新版本1.73.1版本
 
- 1 web应用：所要被监控的web项目
- 2 javamelody-collector-server-1.73.1.war：
        需要放在Tomcat的webapps目录下
- 3 需要的两个jar包，位于zip包里面。
    javamelody-core-1.73.1.jar          说明：每个版本迭代的核心包
    jrobin-1.5.9.1.jar                  说明：监控后台所需要的图形界面包
- 4 资源地址：
    以上资源都统一放在百度网盘上，供需要的同事自行下载
        链接：https://pan.baidu.com/s/1Bo81g9Yn_OiPld_SAgVlTQ 密码：n6pz
 
&nbsp;&nbsp;&nbsp;&nbsp;需要注意的是，JavaMelody监控是非常简单的，部署也很快。通常JavaMelody与应用的整个都是软件自动完成的，并不需要用户做任何的操作。只需要修改一点配置文件即可。监控与应用整合一般都不会超过10秒钟，通常都会自动的被编译环境发现：你需要做的知识拷贝两个jar包，添加10行xml的代码。如果你发布的应用程序不是一个相对目录，而是war包，那么就需要阅读以下下面的章节了。如果是ear（EJBs）,那么就需要去阅读以下User Guide Advanced的一些相关内容了。
 
# JavaMelody配置
　　1 jar包

&nbsp;&nbsp;&nbsp;&nbsp;在百度网盘的v1.73.1中有两个jar包，一个是javamelody-core-1.73.1.jar，另一个是jrobin-1.5.9.1.jar。拷贝这两个jar包到webapp中对应war包的WEB-INF/lib目录下。或者使用Maven，添加javamelody-core 依赖文件pom.xml。
> Maven依赖：
```
<dependency>
    <groupId>net.bull.javamelody</groupId>
    <artifactId>javamelody-core</artifactId>
    <version>1.60.0</version>
</dependency>
```

　　2 web.xml文件

&nbsp;&nbsp;&nbsp;&nbsp;如果你的servletAPI是3.0的，想tomcat7 glassfish v3 jboss6等等，那么就需要配置xml了。不然的话，需要在应用war包的web.xml中添加如下的filter
```
　  <filter>
 
               <filter-name>monitoring</filter-name>
 
               <filter-class>net.bull.javamelody.MonitoringFilter</filter-class>
 
    </filter>
 
   <filter-mapping>
 
           <filter-name>monitoring</filter-name>
 
           <url-pattern>/*</url-pattern>
 
   </filter-mapping>
 
   <listener>
 
           <listener-class>net.bull.javamelody.SessionListener</listener-class>
 
   </listener> 
```
 

　　如果是servlet3.0，还需要添加<async-supported>true</async-supported> 来支持异步请求

 

# 查看监控结果
 

　　现在就可以启动应用服务器打开网址查看监控效果了。

网址：http://<host>/<context>/monitoring

* <host>是web应用服务器的部署IP，通常是localhost:8080 或者127.0.0.1:8080具体看你自己的应用服务器
* <context>是你的web应用的名字。

# 注意事项：

　　如果在启动过程中出错，出错信息含有window server，那么检查一下你是否使用了其他版本的server。

　　并且添加系统参数-Djava.awt.headless=true如果使用到额是tomcat，那么在conf/catalina.properties中添加java.awt.headless=true

然后重启服务器。

# JavaMelody初探
    
    我们在前台网址访问的所有请求，都会产生记录，最终被JavaMelody捕捉到，那个这些记录被保存在哪呢？
    
　　在Tomcat的temp目录下会发现一个javamelody文件夹，在该文件夹内就会发现一个和JavaMelody网页上同名的一个文件夹，比如：
　　![22](https://note.youdao.com/yws/public/resource/3135f4ced8cd7e14b0505e81d841e04a/9E4030E43DBF439DAC6FA8283DE8353B?ynotemdtimestamp=1533863135223)
　　![33](https://note.youdao.com/yws/public/resource/3135f4ced8cd7e14b0505e81d841e04a/D40F154ADAC149E3BF6D319F62918F1F?ynotemdtimestamp=1533863135223)

　　如果我们删除这两个文件，再次启动tomcat,可以发现数据清空了。

　　这也就证明所有的记录的监控信息都在这个文件夹中，那么都有什么呢？

&nbsp;&nbsp;&nbsp;&nbsp;虽然都是RRD的文件，无法直接读取，但是从名字就可以看到它都记录什么数据。比如sql 线程数，内存等等。</br>
后面会继续研究对多种项目的监控，以及源码。最后，附上一些学习网址供大家学习：
> - 本文的参考地址：</br>
https://blog.csdn.net/toker_lizi/article/details/74262659
> - JavaMelody使用和监控报告解读:</br>
https://blog.csdn.net/toker_lizi/article/details/74262659
> - 使用javamelody监控web程序集成总结:</br>
https://blog.csdn.net/zhousenshan/article/details/79056756
> - Springboot整合javamelody：</br>
https://blog.csdn.net/yuppy/article/details/80645667
> - javamelody工具配置总结(包含安全访问等):</br>
https://arstercz.com/javamelody%E5%B7%A5%E5%85%B7%E9%85%8D%E7%BD%AE%E6%80%BB%E7%BB%93/
            
[^1]: 注：本文档仅限内部流传，请勿外传！       