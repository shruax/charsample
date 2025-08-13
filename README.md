# 察语言示例代码库

本仓库包含了察语言（Charlang）的循序渐进的各种示例代码。

# 察语言简介

[察语言（Charlang）](https://topget.org/charlang)是一种快速、动态的脚本语言，可以独立运行，也可以嵌入到Go语言应用程序中运行。 察语言在虚拟机上先编译为字节码再执行，速度优于一般的解释型语言。察语言基于Go语言编写，在语法上非常接近于Go语言，一定程度上可以看做提高了易用性和方便性的Go语言，例如：察语言去除了一些Go语言强制的书写要求、去除了强类型语言的一些限制、引入了一般语言常用的try-catch-finally组合取代Go语言基于defer的异常处理机制等。

# 察语言的特性

- 单个可执行文件的主程序，即可高速运行所有察语言脚本代码；
- 基于纯Go语言编写，无需依赖CGO；
- 跨平台运行，支持Windows、Linux、Mac等主流操作系统；
- 丰富的、可扩展的内置函数，可以处理大多数常见编码场景的需求；
- 易于扩展，如果内置函数无法满足需求，就扩展它（这也是察语言官方推荐的方式，尽量保持简洁，扩展内置函数而非使用模块，虽然察语言支持模块式写法）！
- 除基础数据类型和对象外，提供更丰富的对象：Byte、BigInt、BigFloat、Database、Seq、OrderedMap、Image、Delegate、EvalMachine、Any等，并且类似内置函数，可以按规范自行扩展增改；
- 提供并发/多线程支持；
- 支持图形（GUI）编程；
- 内置文本和图形代码编辑器；
- 提供交互式编程环境（REPL），主程序直接不带参数运行即可启动交互式编程环境，可直接输入代码，并支持多行代码（以“\”分隔）
- 支持以系统服务模式运行，可在后台执行定时任务、进行系统监控等；
- 支持服务器模式运行，内置WEB、应用、微服务三合一服务器，可以处理HTTP请求、提供静态WEB资源服务、提供类似PHP/JSP/ASP的动态页面服务、访问数据库进行存取、进行协议转换等，并支持但语句启动SOCKS或透明代理服务器；
- 代码以纯文本方式分发，也可以进行编译生成单个可执行文件进行分发，解决源代码泄露的顾虑；

# 相关链接

察语言的官网地址在 [这里](https://topget.org/charlang) 。建议从官网下载各个操作系统对应的可执行程序包。

察语言的Github库在 [这里](https://github.com/topxeq/charlang) 。如果需要自行编译或拓展察语言功能，可以从这里开始。

各支持系统的快速下载链接：

- [Windows x64](https://topget.org/pub/char.zip)
- [Windows x64(无终端窗口版，一般用于窗口GUI应用)](https://topget.org/pub/charw.zip)
- [Linux Amd64](https://topget.org/pub/char.tar.gz)
- [Linux Arm8(Termux)](https://topget.org/pub/charArm8.tar.gz)

# 快速入门

## 快速安装与使用

- 从官网下载对应操作系统的察语言主程序压缩包，解压后即可使用，建议将主程序所在的路径加入系统路径，或直接将主程序（char.exe或char）放在某个已经在系统路径内的文件夹下。
- 不带参数直接运行主程序即可进入察语言的交互式编程环境（REPL）。

```shell
D:\tmpx>char
Charlang 1.9.6 by TopXeQ
> 1.8 * 3.79
6.822
> a := 12
> pln(a + 19) 
31
> for i in 3 {\
    pln(i, i+1)\
  }
0 1
1 2
2 3
> q

D:\tmpx>
```

如上所示，在交互式编程环境中，可以直接输入察语言中的表达式进行计算并获得结果值，也可以输入语句执行，也可以输入多行代码（未结束前以“\”作为每行的结尾）执行。输入“q”可以退出察语言交互式编程环境，或者直接按Ctrl-C中断REPL也可以。

- 运行主程序时加上代码文件（脚本）作为参数，即可执行该文件中的察语言代码。察语言代码文件一般后缀为“.char”。

```shell
D:\tmpx>char test.char
aaa[3]

D:\tmpx>
```

## 从源码编译执行察语言

如果需要编译其他操作系统下的察语言（例如在某些未提供察语言可执行程序包的操作系统下使用，这种方式支持所有Go语言支持的操作系统），或者需要修改或拓展察语言的功能，可以下载[Github仓库](https://github.com/topxeq/charlang)上的察语言源码进行修改和编译。这种方式需要先安装好Go语言开发环境。

```shell
go get -u github.com/topxeq/charlang
```

或

```shell
cd gosrc/github.com/topxeq

git clone github.com/topxeq/tkc

git clone github.com/topxeq/charlang

cd charlang/cmd

go install

char

```


## 各种运行察语言的方式

- 不带参数将直接启动察语言交互式编程环境： `./char`；
- 运行某个源文件中的代码： `char d:\scripts\test.char`；
- 运行系统剪贴板中的代码（将文字视作代码执行）： `char -clip`；
- 从远程网址链接中执行代码： `char -remote http://replacewithyourdomain.com/script/abc.char`；
- 执行察语言的例子代码：`char -example basic.char`；
- 直接从Go语言源代码目录（例如`d:\gosrc\github.com\topxeq\charlang\cmd\scripts\basic.char`）执行代码： `char -gopath basic.char`
- 从在配置文件中指定的本地目录中执行：在用户目录的char子目录下放置一个local.cfg文件，其中指定本功能的根目录，例如 `c:\scripts`，然后执行 `char -local basic.char` 将执行 'c:\scripts\basic.char'；
- 从远程/云端快捷执行：在用户目录的char子目录下放置一个cloud.cfg文件，其中指定本功能的根目录，例如 `http://script.my.com/` ，然后执行 `char -cloud basic.char` 将等同于 `char -remote http://script.my.com/basic.char`；
- 选择代码文件并执行： `char -selectScript`；
- 启动内置多行文本编辑器编辑后再执行： `char -cedit d:\scripts\test.char`，然后按 Ctrl-Q 执行输入的代码，Ctrl-X 退出；
- 在内置图形编辑器（目前仅支持Windows）中编辑代码执行： `char -edit d:\scripts\test.char`；
- 在Go语言中作嵌入式引擎运行，可参考cmd子目录中的代码；
- 在其他任何语言中通过DLL调用（仅支持Windows）；
- 作为系统服务运行（需要管理员或root用户权限）： `char -reinstallService`；


