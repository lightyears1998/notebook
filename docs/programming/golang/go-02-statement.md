# Go 语句

## 表达式

### 声明

1. `var`可用于声明变量；简洁赋值语句`:=`可在类型明确时代替`var`，但只能在函数内使用。（在函数外的语句只能由关键字起首。）
2. 没有明确初始值的变量会自动被赋予零值。
3. 类型名在变量名之后，如果多个变量类型相同，则除最后一个外，其他类型说明可以省略。

`fmt.Printf("类型名：%T，值：%v", variable, variable)`

1. 常量使用`const`声明，不能使用简洁赋值语句来声明常量。
2. 常量由上下文来决定具体类型。（数值常量总是高精度的值。）

### `defer`

`defer`语句使后面的函数推迟到外层函数结束后调用；但函数的参数会被立即求值。

注意如果存在多条`defer`语句，则后面的`defer`语句会先执行。（后进先出顺序）

## 分支语句

### `if`

``` go
if 7%2 == 0 {
    fmt.Println("7 is even")
} else {
    fmt.Println("7 is odd")
}

// 可在 `if` 的条件表达式前执行一个简单语句，
// 简单语句中声明的变量的作用域在整个 `if-else` 语句块中可用。
if num := 9; num < 0 {
    fmt.Println(num, "is negative")
} else if num < 10 {
    fmt.Println(num, "has 1 digit")
} else {
    fmt.Println(num, "has multiple digits")
}
```

### `switch`

1. `case`无需为常量，取值不必为整数。`switch`是书写多条`if`语句的清晰方式。
2. 无需提供`break`语句，除非以`fallthrough`语句结尾，否则分支会自动终止。
3. 从上而下顺次执行，直到匹配成功为止。
4. 无条件的`switch`相当于`switch true`，能将一连串的if-else-then写得更简洁。

## 循环语句

### `for`

只使用`for`循环。C语言中的`while`在Go中为`for`。

`for`语句的三部分由`;`隔开，花括号是必须的。

无限循环可简写为`for {}`。
