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

## 变量与常量

1. `var`可用于声明变量；简洁赋值语句`:=`可在类型明确时代替`var`，但只能在函数内使用。
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

---

## 指南

- [A Tour of Go](https://tour.go-zh.org/)

---

## 安装

待安装
