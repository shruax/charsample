# 察语言文档及示例代码库

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
- 获取数据类型的编码或名称 [sample01.006.char](https://github.com/shruax/charsample/blob/main/sample01.006.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample01.006.char)

### 常见数据类型详解

在察语言中，对象类也可以理解成数据类型（实际上，察语言内部也是将数据类型全部封装成对象的），例如布尔数据类型我们可以理解为布尔对象类，而布尔类型的的值或变量，我们都可以称之为一个布尔对象（实例）。后面说明中常会混用这几种说法，应该都好理解，不再重复说明。

- undefined数据类型 [sample02.001.char](https://github.com/shruax/charsample/blob/main/sample02.001.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.001.char)
- 布尔数据类型 [sample02.002.char](https://github.com/shruax/charsample/blob/main/sample02.002.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.002.char)
- 整数数据类型 [sample02.003.char](https://github.com/shruax/charsample/blob/main/sample02.003.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.003.char)
- 浮点数数据类型 [sample02.004.char](https://github.com/shruax/charsample/blob/main/sample02.004.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.004.char)
- 字节数据类型 [sample02.005.char](https://github.com/shruax/charsample/blob/main/sample02.005.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.005.char)
- 字符数据类型 [sample02.006.char](https://github.com/shruax/charsample/blob/main/sample02.006.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.006.char)
- 字符串、字节数组与字符数组 [sample02.007.char](https://github.com/shruax/charsample/blob/main/sample02.007.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.007.char)
- 数组与切片 [sample02.008.char](https://github.com/shruax/charsample/blob/main/sample02.008.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.008.char)
- 映射与有序映射 [sample02.009.char](https://github.com/shruax/charsample/blob/main/sample02.009.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample02.009.char)

### 流程控制与跳转

- 循环及其控制 [sample03.001.char](https://github.com/shruax/charsample/blob/main/sample03.001.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample03.001.char)
- 条件判断分支 [sample03.002.char](https://github.com/shruax/charsample/blob/main/sample03.002.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample03.002.char)

### 函数相关

- 函数的（输入）参数 [sample04.001.char](https://github.com/shruax/charsample/blob/main/sample04.001.char)  [RAW](https://raw.githubusercontent.com/shruax/charsample/refs/heads/main/sample04.001.char)

## 对象（类）列表及说明

### undefined

undefined 是一个特殊的对象，表示没有赋值的值，或者某个函数没有返回值等含义。具体使用请参看 [例子](https://github.com/shruax/charsample/blob/main/sample02.001.char)

### bool

布尔 bool 类型的对象的说明请参看 [例子](https://github.com/shruax/charsample/blob/main/sample02.002.char)

### string

字符串 string 类型的对象的说明请参看 [例子](https://github.com/shruax/charsample/blob/main/sample02.007.char)

## 常见内置函数列表

### 基础与调试类

#### globals 获取所有全局变量

- 说明：获取所有全局变量，返回值是一个映射（map）对象，包含的键值对即为所有当前的全局变量。
- 用法示例：

```shell
C:\Users\Administrator>char
Charlang 2.0.1 by TopXeQ
> pln(globals())
{"scriptPathG": "", "runModeG": "repl", "argsG": ["char"], "versionG": "2.0.1"}
>
```

#### getConst 获取预定义常量

- 说明：获取一些系统预定义的常量，例如数学上的π值、e值等，更多的可取常量请参考后面的预定异常量一节。
- 用法示例：

```shell
C:\Users\Administrator>char
Charlang 2.0.1 by TopXeQ
> plt(getConst("math.Pi"))
(float)3.141592653589793
25
> plt(getConst("math.E")) 
(float)2.718281828459045
25
>
```

#### callMethod 调用对象的方法

- 说明：调用察语言对象的方法。借用面向对象的概念，察语言中的任何数据类型也都可以看作是一个对象，对象一般具有方法（即函数），方法可以用小数点的写法来调用，也可以使用内置函数 callMethod 来调用。
- 用法示例：

```shell
C:\Users\Administrator>char
Charlang 2.0.7 by TopXeQ
> a := [1, 2]
> a.size()
2
> callMethod(a, "size")
2
> callMethod(a, "remove", 1)
[1]
> a
[1, 2]
>
```

注意，上面例子中，`a.size()` 等价于 `callMethod(a, "size")` 的写法。

#### mt 等价于 callMethod

#### callNamedFunc 调用预定义Go语言函数

- 说明：调用一些Go语言函数，一般用于扩展察语言功能。注意，并非Go语言中所有包都可以直接被调用，只有在察语言中明确声明过的某些包中的函数才能被这样调用，具体可调用的请参看后面预定义可调用的Go语言函数一节。
- 用法示例：

```go
// 获取常用的tk对象，注意内置函数callNamedFunc返回的是一个数组，这是为了适应某些Go语言函数具有多个返回值的情况
tk := callNamedFunc("tk.NewTK")[0]

pln(tk)

// 调用tk对象的GetTextSimilarity方法
// 注意callMethodEx内置函数返回的也是一个数组，原因也是为了适应某些Go语言函数具有多个返回值的情况
rs := callMethodEx(tk, "GetTextSimilarity", "abc", "abd")[0]

plt(rs)

// 调用Go语言中time.Now()函数
// 注意，并非Go语言中所有包都可以直接被调用，只有在察语言中明确声明过的某些包中的函数才能被这样调用
time1 := callNamedFunc("time.Now")[0]

plt(time1)

// 调用Go语言中time.Time对象的AddDate方法，获取当前时间的前一个月的时间
time2 := callMethodEx(time1, "AddDate", 0, -1, 0)[0]

plt(time2)

```

#### callMethodEx 调用Go语言对象的方法

- 说明：对于调用callNamedFunc函数返回的Go语言对象，调用它的方法函数。具体用法参看 callNamedFunc 函数的说明。

#### mtEx 等价于 callMethodEx

#### len 获取对象长度（字符串长度、数组项个数、映射项个数等）

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

### 数据类型相关

#### typeCode 获取数据类型编码

- 说明：获取支持任意数据、常量或变量的数据类型的编码，返回值是一个整数值。
- 用法示例：

```go
a := 1

pl("typeCode of a: %v", typeCode(a))

```

#### typeName 获取数据类型名称

- 说明：获取支持任意数据、常量或变量的数据类型的名称，返回值是一个字符串。
- 用法示例：

```go
a := 1

pl("typeName of a: %v", typeName(a))

```

#### typeof 获取数据类型名称

- 说明：等价于typeName。

#### typeOfAny 获取any类型数据的实际类型

- 说明：获取any类型数据中实际的数据类型（该数据在察语言中如果存在，则返回该数据类型名称，否则返回Go语言中的数据类型），返回值是一个字符串。
- 用法示例：

```shell
a := any()

pl("typeOfAny of a: %v", typeOfAny(a))

```

## 专题与杂项

### 预定义的全局变量

- versionG: 当前察语言（Charlang）的版本号
- basePathG: 察语言的根路径，一般是当前系统登录用户的用户根目录，例如 c:\Users\Administrator ；当察语言作为系统服务运行时，一般是系统的根目录下的char目录，例如 Windows 下的 c:\char 或 Linux 下的 /char
- argsG: 运行察语言主程序时的命令行参数，数组类型，其中每一项都是字符串
- scriptPathG: 察语言当前运行的脚本（源代码）文件的路径
- runModeG: 当前察语言的运行模式，例如 script, repl, service, charms, chp, chardc 等

当察语言运行在服务（器）模式下（即以WEB/应用/微服务多合一服务器模式运行）时，特定的预定义全局变量：variables:

- requestG: HTTP请求对象，包含该次请求的各种信息
- responseG: HTTP响应对象，处理HTTP请求时将基于HTTP响应对象进行设置响应头、写响应体等操作
- reqUriG: HTTP请求的URI，例如 “static/images/img001.png”
- paraMapG: HTTP请求中的 GET/POST 参数，是一个映射对象，类似 `{"auth": "xxxxx", "input1": "value1"}`

Windows 操作系统下，特定的预定义全局变量：

- guiG: 其中保存一个连接至系统的WebView2组件的对象，可以用于启动和操控图形界面

### 预定义的一些常量

```go
"tk.TimeFormat":            tk.TimeFormat,            // "2006-01-02 15:04:05"
"tk.TimeFormatMS":          tk.TimeFormatMS,          // "2006-01-02 15:04:05.000"
"tk.TimeFormatMSCompact":   tk.TimeFormatMSCompact,   // "20060102150405.000"
"tk.TimeFormatCompact":     tk.TimeFormatCompact,     // "20060102150405"
"tk.TimeFormatCompact2":    tk.TimeFormatCompact2,    // "2006/01/02 15:04:05"
"tk.TimeFormatDateCompact": tk.TimeFormatDateCompact, // "20060102"

"time.Layout":   time.Layout,
"time.RFC1123":  time.RFC1123,
"time.RFC3339":  time.RFC3339,
"time.DateTime": time.DateTime,
"time.DateOnly": time.DateOnly,
"time.TimeOnly": time.TimeOnly,

"time.Millisecond": time.Millisecond,
"time.Second": time.Second,
"time.Minute": time.Minute,
"time.Hour": time.Hour,

"math.Pi":   math.Pi,
"math.E":   math.E,

"maxInt":   math.MaxInt,
"minInt":   math.MinInt,
"maxFloat": math.MaxFloat64,
"minFloat": math.SmallestNonzeroFloat64,
"math.MaxInt":   math.MaxInt,
"math.MinInt":   math.MinInt,
"math.MaxFloat": math.MaxFloat64,
"math.MinFloat": math.SmallestNonzeroFloat64,


"http.StatusContinue":           100, // RFC 9110, 15.2.1
"http.StatusSwitchingProtocols": 101, // RFC 9110, 15.2.2
"http.StatusProcessing":         102, // RFC 2518, 10.1
"http.StatusEarlyHints":         103, // RFC 8297

"http.StatusOK":                   200, // RFC 9110, 15.3.1
"http.StatusCreated":              201, // RFC 9110, 15.3.2
"http.StatusAccepted":             202, // RFC 9110, 15.3.3
"http.StatusNonAuthoritativeInfo": 203, // RFC 9110, 15.3.4
"http.StatusNoContent":            204, // RFC 9110, 15.3.5
"http.StatusResetContent":         205, // RFC 9110, 15.3.6
"http.StatusPartialContent":       206, // RFC 9110, 15.3.7
"http.StatusMultiStatus":          207, // RFC 4918, 11.1
"http.StatusAlreadyReported":      208, // RFC 5842, 7.1
"http.StatusIMUsed":               226, // RFC 3229, 10.4.1

"http.StatusMultipleChoices":  300, // RFC 9110, 15.4.1
"http.StatusMovedPermanently": 301, // RFC 9110, 15.4.2
"http.StatusFound":            302, // RFC 9110, 15.4.3
"http.StatusSeeOther":         303, // RFC 9110, 15.4.4
"http.StatusNotModified":      304, // RFC 9110, 15.4.5
"http.StatusUseProxy":         305, // RFC 9110, 15.4.6

"http.StatusTemporaryRedirect": 307, // RFC 9110, 15.4.8
"http.StatusPermanentRedirect": 308, // RFC 9110, 15.4.9

"http.StatusBadRequest":                   400, // RFC 9110, 15.5.1
"http.StatusUnauthorized":                 401, // RFC 9110, 15.5.2
"http.StatusPaymentRequired":              402, // RFC 9110, 15.5.3
"http.StatusForbidden":                    403, // RFC 9110, 15.5.4
"http.StatusNotFound":                     404, // RFC 9110, 15.5.5
"http.StatusMethodNotAllowed":             405, // RFC 9110, 15.5.6
"http.StatusNotAcceptable":                406, // RFC 9110, 15.5.7
"http.StatusProxyAuthRequired":            407, // RFC 9110, 15.5.8
"http.StatusRequestTimeout":               408, // RFC 9110, 15.5.9
"http.StatusConflict":                     409, // RFC 9110, 15.5.10
"http.StatusGone":                         410, // RFC 9110, 15.5.11
"http.StatusLengthRequired":               411, // RFC 9110, 15.5.12
"http.StatusPreconditionFailed":           412, // RFC 9110, 15.5.13
"http.StatusRequestEntityTooLarge":        413, // RFC 9110, 15.5.14
"http.StatusRequestURITooLong":            414, // RFC 9110, 15.5.15
"http.StatusUnsupportedMediaType":         415, // RFC 9110, 15.5.16
"http.StatusRequestedRangeNotSatisfiable": 416, // RFC 9110, 15.5.17
"http.StatusExpectationFailed":            417, // RFC 9110, 15.5.18
"http.StatusTeapot":                       418, // RFC 9110, 15.5.19 (Unused)
"http.StatusMisdirectedRequest":           421, // RFC 9110, 15.5.20
"http.StatusUnprocessableEntity":          422, // RFC 9110, 15.5.21
"http.StatusLocked":                       423, // RFC 4918, 11.3
"http.StatusFailedDependency":             424, // RFC 4918, 11.4
"http.StatusTooEarly":                     425, // RFC 8470, 5.2.
"http.StatusUpgradeRequired":              426, // RFC 9110, 15.5.22
"http.StatusPreconditionRequired":         428, // RFC 6585, 3
"http.StatusTooManyRequests":              429, // RFC 6585, 4
"http.StatusRequestHeaderFieldsTooLarge":  431, // RFC 6585, 5
"http.StatusUnavailableForLegalReasons":   451, // RFC 7725, 3

"http.StatusInternalServerError":           500, // RFC 9110, 15.6.1
"http.StatusNotImplemented":                501, // RFC 9110, 15.6.2
"http.StatusBadGateway":                    502, // RFC 9110, 15.6.3
"http.StatusServiceUnavailable":            503, // RFC 9110, 15.6.4
"http.StatusGatewayTimeout":                504, // RFC 9110, 15.6.5
"http.StatusHTTPVersionNotSupported":       505, // RFC 9110, 15.6.6
"http.StatusVariantAlsoNegotiates":         506, // RFC 2295, 8.1
"http.StatusInsufficientStorage":           507, // RFC 4918, 11.5
"http.StatusLoopDetected":                  508, // RFC 5842, 7.2
"http.StatusNotExtended":                   510, // RFC 2774, 7
"http.StatusNetworkAuthenticationRequired": 511, // RFC 6585, 6

```

### 预定义可调用的Go语言函数

注意，目前可调用的函数还不多，主要是提供一个给开发者可自行快速扩展察语言的能力。

```
"fmt.Fprintf": fmt.Fprintf,
"tk.NewTK":    tk.NewTK,
"time.Now":    time.Now,

```