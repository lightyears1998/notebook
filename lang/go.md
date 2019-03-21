# GoLang

## 控制语句

### `for`

只使用`for`循环。C语言中的`while`在Go中为`for`。

`for`语句的三部分由`;`隔开，花括号是必须的。

无限循环可简写为`for { /* statements */ }`

### `if`

可在`if`的条件表达式前执行一个简单语句（就像`for`语句中的第一部分），简单语句中声明的变量的作用域在`if-else`语句块中可用。

### `switch`

`case`无需为常量，取值不必为整数。`switch`是书写多条`if`语句的清晰方式。

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

---

## 指南

- [A Tour of Go](https://tour.go-zh.org/)

---

## 安装

待安装
