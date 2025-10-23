# 察语言示例代码库

本仓库包含了察语言（Charlang）的中文文档与循序渐进的各种示例代码。

## 察语言简介

[察语言（Charlang）](https://topget.org/charlang)是一种快速、动态的脚本语言，可以独立运行，也可以嵌入到Go语言应用程序中运行。 察语言在虚拟机上先编译为字节码再执行，速度优于一般的解释型语言。察语言基于Go语言编写，在语法上非常接近于Go语言，一定程度上可以看做提高了易用性和方便性的Go语言，例如：察语言去除了一些Go语言强制的书写要求、去除了强类型语言的一些限制、引入了一般语言常用的try-catch-finally组合取代Go语言基于defer的异常处理机制等。

## 察语言的特性

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

## 相关链接

察语言的官网地址在 [这里](https://topget.org/charlang) 。建议从官网下载各个操作系统对应的可执行程序包。

察语言的Github库在 [这里](https://github.com/topxeq/charlang) 。如果需要自行编译或拓展察语言功能，可以从这里开始。

察语言支持的各个操作系统的主程序压缩包快速下载链接：

- [Windows x64](https://topget.org/pub/char.zip)
- [Windows x64(无终端窗口版，一般用于窗口GUI应用)](https://topget.org/pub/charw.zip)
- [Linux Amd64](https://topget.org/pub/char.tar.gz)
- [Linux Arm8(Termux)](https://topget.org/pub/charArm8.tar.gz)

[察语言的Golang包文档地址](https://pkg.go.dev/github.com/topxeq/charlang)

[英文版内置函数参考](https://topget.org/dc/charlang/funcs)

## 快速入门

### 快速安装与使用

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

### 从源码编译执行察语言

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


### 各种运行察语言的方式

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
- 在Go语言中作嵌入式脚本引擎运行，可参考察语言源码仓库中cmd子目录中的代码，或者参看本节后面的详细说明；
- 将脚本编译为一个可执行文件执行（Windows下如果仅希望显示图形界面而不需要命令行窗口，需要使用察语言的GUI版，即名为charw.exe的主程序来进行脚本编译），详见本节后面的详细说明；
- 在其他任何语言中通过DLL调用（仅支持Windows）；
- 作为系统服务运行（需要管理员或root用户权限）： `char -reinstallService`；
- 作为一个3合1服务器（WEB、应用、微服务）运行： `char -server` 或 `char -server -certDir=/datax/cert -webDir=/datax/xweb -dir=/datax/ms -port=80 -sslPort=443`

#### 将脚本编译为一个可执行文件执行

```shell
D:\tmp>char -compile -output=basic.exe -example basic.char

D:\tmpx>basic.exe
3.4000000000000004

D:\tmpx>basic
3.4000000000000004

```

#### Windows下将脚本编译为无命令行窗口仅图形GUI的单个可执行文件

在Windows中使用察语言的GUI版主程序charw.exe编译脚本，以避免在运行时显示控制台窗口（CMD）。例如：

```shell

charw -compile -output=cal.exe -example guiCalculator.char

D:\tmpx>cal.exe

```

#### 在Go语言中作嵌入式脚本引擎运行察语言脚本

要在Go语言（Golang） 中运行察语言（Charlang）脚本，必须先把脚本编译为一个 `Bytecode` 对象，然后才能由察语言虚拟机（VM）执行。察语言默认启用了一个简单的优化器
来进行编译，优化器会将不影响代码执行的简单表达式替换为常数值。请注意，可以禁用此选项来加快编译过程。

注意，察语言还在活跃开发阶段，因此为了顺利编译下面的代码，需要在 `$GOPATH/src/github.com/topxeq` 目录（Windows下为 `%GOPATH%/src/github.com/topxeq` ）下先执行 `git clone https://github.com/topxeq/tkc` ，然后修改本代码目录的 go.mod 文件，在其中增加 `replace github.com/topxeq/tkc v0.0.0 => $GOPATH/src/github.com/topxeq/tkc` 一行，注意修改上面的 `$GOPATH` 为当前系统中Go语言的GOPATH变量指向的实际目录。

```go
package main

import (
  "fmt"

  "github.com/topxeq/charlang"
)

func main() {
  script := `
  param num

  var fib
  fib = func(n, a, b) {
    if n == 0 {
      return a
    } else if n == 1 {
      return b
    }
    return fib(n-1, b, a+b)
    }
  return fib(num, 0, 1)
  `
  
  bytecode, err := charlang.Compile([]byte(script), &charlang.DefaultCompilerOptions)

  if err != nil {
    panic(err)
  }

  retValue, err := charlang.NewVM(bytecode).Run(nil,  charlang.Int(35))

  if err != nil {
    panic(err)
  }

  fmt.Println(retValue) // 9227465
}
```

VM的执行可以通过使用`Abort`方法中止，这将导致`Run`方法返回一个错误，该错误包装了 `ErrVMAborted` 错误。`Abort` 必须从另一个不同的goroutine中调用，多次调用是安全的。

从 `Run` 方法返回的错误可以通过以下方式检查特定的错误值：Go 语言中，`errors` 包提供了 `errors.Is` 函数，用于判断一个错误是否为指定类型的错误。

`VM`实例是可复用的。`VM`的`Clear`方法会清除所有持有的引用并确保堆栈和模块缓存被清理。

```go
vm := charlang.NewVM(bytecode)

retValue, err := vm.Run(nil,  Charlang.Int(35))

/* 可以执行Clear方法以清除运行数据 */
// vm.Clear()

retValue, err := vm.Run(nil,  Charlang.Int(34))
/* ... */
```

全局变量可以通过`global`关键字声明并提供给VM。这样脚本就可以访问全局变量。一般应使用类似Map的对象来获取/设置全局变量，如下所示。

```go
script := `
param num

global upperBound

return num > upperBound ? "big" : "small"
`

bytecode, err := charlang.Compile([]byte(script), &charlang.DefaultCompilerOptions)

if err != nil {
  panic(err)
}

g := charlang.Map{"upperBound": charlang.Int(1984)}

retValue, err := charlang.NewVM(bytecode).Run(g, charlang.Int(2018))

// retValue == charlang.String("big")
```

从上面的例子可以看出，VM的`Run`方法接受多个参数，第一个为全局变量globals，它是一个映射（Map）类型的，在其中用键值对来供脚本中的global关键字来声明后即可使用，传递 `nil` 值表示不适用全局变量。`args`可变参数允许向VM提供任意数量的参数，这些参数通过 `param` 关键字来访问。

```go
func (vm *VM) Run(globals Object, args ...Object) (Object, error)
```

下面是另一个较完整的例子，包含了全局变量、可变输入参数、数组、循环、 `try...catch...finally` 结构等，前文未涉及的概念具体可参看后面章节里例子中的详细说明：

```go
package main

import (
    "fmt"

    "github.com/topxeq/charlang"
)

func main() {
    script := `
param ...args

mapEach := func(seq, fn) {

    if !isArray(seq) {
        return error("want array, got " + typeName(seq))
    }

    var out = []

    if sz := len(seq); sz > 0 {
        out = repeat([0], sz)
    } else {
        return out
    }

    try {
        for i, v in seq {
            out[i] = fn(v)
        }
    } catch err {
        println(err)
    } finally {
        return out, err
    }
}

global multiplier

v, err := mapEach(args, func(x) { return x*multiplier })
if err != undefined {
    return err
}

return v
`

    bytecode, err := charlang.Compile([]byte(script), &charlang.DefaultCompilerOptions)
    if err != nil {
        panic(err)
    }
    
    globals := charlang.Map{"multiplier": charlang.Int(2)}
    
    ret, err := charlang.NewVM(bytecode).Run(
        globals,
        charlang.Int(1), charlang.Int(2), charlang.Int(3), charlang.Int(4),
    )
    
    if err != nil {
        panic(err)
    }
    
    fmt.Println(ret) // [2, 4, 6, 8]
}
```


## 例子代码索引

注意，每个代码例子中都有详细的注释说明，帮助理解察语言中的各种概念、功能与用法等。

### 基础示例

- Hello world! [sample01.001.char](https://github.com/shruax/charsample/blob/main/sample01.001.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample01.001.char)
- 基本赋值与计算 [sample01.002.char](https://github.com/shruax/charsample/blob/main/sample01.002.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample01.002.char)
- 注释的写法 [sample01.003.char](https://github.com/shruax/charsample/blob/main/sample01.003.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample01.003.char)
- 变量的类型、声明与赋值 [sample01.004.char](https://github.com/shruax/charsample/blob/main/sample01.004.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample01.004.char)
- 函数的声明与使用（递归法计算斐波那契数列） [sample01.005.char](https://github.com/shruax/charsample/blob/main/sample01.005.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample01.005.char)

### 常见数据类型详解

在察语言中，对象类也可以理解成数据类型（实际上，察语言内部也是将数据类型全部封装成对象的），例如布尔数据类型我们可以理解为布尔对象类，而布尔类型的的值或变量，我们都可以称之为一个布尔对象（实例）。后面说明中常会混用这几种说法，应该都好理解，不再重复说明。

- undefined数据类型 [sample02.001.char](https://github.com/shruax/charsample/blob/main/sample02.001.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.001.char)
- 布尔数据类型 [sample02.002.char](https://github.com/shruax/charsample/blob/main/sample02.002.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.002.char)
- 整数数据类型 [sample02.003.char](https://github.com/shruax/charsample/blob/main/sample02.003.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.003.char)
- 浮点数数据类型 [sample02.004.char](https://github.com/shruax/charsample/blob/main/sample02.004.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.004.char)
- 字节数据类型 [sample02.005.char](https://github.com/shruax/charsample/blob/main/sample02.005.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.005.char)
- 字符数据类型 [sample02.006.char](https://github.com/shruax/charsample/blob/main/sample02.006.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.006.char)
- 字符串、字节数组与字符数组 [sample02.007.char](https://github.com/shruax/charsample/blob/main/sample02.007.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.007.char)

### 流程控制与跳转

- 循环及其控制 [sample03.001.char](https://github.com/shruax/charsample/blob/main/sample03.001.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample03.001.char)
- 条件判断分支 [sample03.002.char](https://github.com/shruax/charsample/blob/main/sample03.002.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample03.002.char)

## 对象（类）列表及说明

### undefined

undefined 是一个特殊的对象，表示没有赋值的值，或者某个函数没有返回值等含义。具体使用请参看 [例子](https://github.com/shruax/charsample/blob/main/sample02.001.char)

### bool

布尔 bool 类型的对象的说明请参看 [例子](https://github.com/shruax/charsample/blob/main/sample02.002.char)

## 常见内置函数列表

### 基础与调试类

### globals

- 说明：获取所有全局变量，返回值是一个映射（map）对象，包含的键值对即为所有当前的全局变量。
- 用法示例：

```shell
C:\Users\Administrator>char
Charlang 2.0.1 by TopXeQ
> pln(globals())
{"scriptPathG": "", "runModeG": "repl", "argsG": ["char"], "versionG": "2.0.1"}
>
```

### len

- 说明：获取支持该函数的各种值、变量或对象等的长度或实际含量等，例如可以获取字符串的长度、数组的元素个数、映射的键值对数量等，返回值是一个整数值。
- 用法示例：

```shell
C:\Users\Administrator>char
Charlang 2.0.1 by TopXeQ
> len("abc123")
6
> len(["a", "b", 1.2])
3
> len1 := len({"field1": "value1", "field2": "value2"})
> pln(len1)
2
>

```

## 专题与杂项

### 