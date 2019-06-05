# GoLang

## 基本结构

```go
package math

import "fmt"

func main() {
    fmt.Println("...")
}
```

## package

每个程序从`main`包开始运行。

```go
// 分组导入语句

import (
    "fmt"
    "math"
)
```

如果标识符以大写开头，即为导出。在包外只能引用已经导出的名字。

## 控制语句

### `for`

只使用`for`循环。C语言中的`while`在Go中为`for`。

`for`语句的三部分由`;`隔开，花括号是必须的。

无限循环可简写为`for { /* statements */ }`

### `if`

可在`if`的条件表达式前执行一个简单语句（就像`for`语句中的第一部分），简单语句中声明的变量的作用域在`if-else`语句块中可用。

### `switch`

1. `case`无需为常量，取值不必为整数。`switch`是书写多条`if`语句的清晰方式。
2. 无需提供`break`语句，除非以`fallthrough`语句结尾，否则分支会自动终止。
3. 从上而下顺次执行，直到匹配成功为止。

### `defer`

`defer`语句使后面的函数推迟到外层函数结束后调用；但函数的参数会被立即求值。

注意如果存在多条`defer`语句，则后面的`defer`语句会先执行。（后进先出顺序）

## 指针

指针保存值在内存中的地址，零值为`nil`。

```go
// 注意声明指针类型时的符号顺序与C++不同。
var p *int
```

```go
i := 42
p := &i
fmt.Println(*p)
```

没有C++中的指针运算。

## 结构体

```go
type Vertex struct {
    X int
    Y int
}
```

注意与C中`typedef known-type alias1, alias2, ...`的差异，这符合Go“类型名在变量名之后”的设计原则。

使用`.`来访问结构体成员。

结构体的指针可以隐式间接引用结构体。对于指针`p`，`(*p).X`与`p.X`是等价的。

```go
// 结构体文法
v1 := Vertex{1, 2}
v2 := Vertex{X = 1}
p1 := &Vertex{1, 2}  // 隐式指针类型
```

## 变量与常量

1. `var`可用于声明变量；简洁赋值语句`:=`可在类型明确时代替`var`，但只能在函数内使用。（在函数外的语句只能由关键字起首。）
2. 没有明确初始值的变量会自动被赋予零值。
3. 类型名在变量名之后，如果多个变量类型相同，则除最后一个外，其他类型说明可以省略。

`fmt.Printf("类型名：%T，值：%v", variable, variable)`

1. 常量使用`const`声明，不能使用简洁赋值语句来声明常量。
2. 常量由上下文来决定具体类型。（数值常量总是高精度的值。）

## 函数

```go
func add(x int, y int) int {
    return x + y
}
```

函数的返回值可被命名。无参的`return`将返回已命名的返回值。

```go
func split(sum int) (x, y int) {
    x = sum * 4 / 9
    y = sum - x
    return
}

func main() {
    fmt.Println(split(17))  // 7 10
}
```

## 数组

`n[T]`表示n个`T`类型的元素的数组。

数组的大小是固定的。

## 切片

`[]T`表示T类型的数组的一个切片。

切片本身不存储数据，只是相应的底层数组的描述。对切片的修改会影响底层数组。

```go
a[1:4]  // 左闭右开区间[1, 4)
```

```go
// 切片文法
[]bool {true, false, true}  // 先创建数组，再创建引用数组的切片
```

---

## 指南

- [A Tour of Go](https://tour.go-zh.org/)

---

## 安装Go的运行环境

## 在Linux上安装Go

<https://www.digitalocean.com/community/tutorials/how-to-install-go-1-7-on-centos-7>

## 包管理`go get`

```sh
go get -flags <package>  # 远程包导入
```

- `<package>`可以是url，也可以是`all`。
- `-fix`
- `-u` update
- `-v` verbose

HTTP代理

```bash
http_proxy=127.0.0.1:8080 go get code.google.com/p/go.crypto/bcrypt  
```

```cmd
set http_proxy=http://[user]:[pass]@[proxy_ip]:[proxy_port]/
set https_proxy=http://[user]:[pass]@[proxy_ip]:[proxy_port]/
```

## 安装常用的工具

```sh
go get -u github.com/mdempsky/gocode
go get -u github.com/uudashr/gopkgs/cmd/gopkgs
go get -u github.com/ramya-rao-a/go-outline
go get -u github.com/acroca/go-symbols
go get -u golang.org/x/tools/cmd/guru
go get -u golang.org/x/tools/cmd/gorename
go get -u github.com/go-delve/delve/cmd/dlv
go get -u github.com/stamblerre/gocode
go get -u github.com/rogpeppe/godef
go get -u github.com/sqs/goreturns
go get -u golang.org/x/lint/golint
```
