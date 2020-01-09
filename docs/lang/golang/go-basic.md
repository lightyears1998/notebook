# Go语言笔记：基础

## TODO

golang.org
play.golang.org
go tour

os.Args

strings.Join()

Map不排序，防止依赖某种序列。

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

## 基本数据类型

与C语言不同，Go在不同数据类型的项之间赋值需要显式类型转换，即使不会发生截断。

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

函数可以返回任意数量的参数。

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

切片`s`拥有长度`len(s)`和容量`cap(s)`。长度是切片所包含的元素的个数；容量是从切片的第一个元素开始，到底层数组末尾的元素个数。

切片的零值是`nil`。`nil`切片的长度和容量都为0，并且没有底层数组。

```go
// 切片可以用`make()`创建，这也是创建动态数组的方式。
a := make([]int, 5)  // len(a) = 5

b := make([]int, 5, 6)  // len(b) = 5, cap(b) = 6
```

```go
// 使用append()向切片追加元素
func append(s []T, vs ...T) []T
```

当切片的底层数组不足以容纳所有给定的值时，Go为会切片分配一个更大的数组，返回的切片会指向这个新分配的数组。

for循环的range形式可以用于遍历切片或映射。每次迭代都会返回两个值。第一个值为当前元素的下标，第二个值为该下标所对应元素的一份副本。可以将下标或值赋予`_`来忽略它。

```go
pow := []int {1, 2, 4, 8, 16}
for i, v range pow {
    fmt.Printf("2**%d == %d", i, v)
}
```

## 映射

映射将键映射到值。

```go
m map[string]Vertex := make(map[string]Vertex)

var m = map[string]Vertex{
    "Bell Labs": Vertex{
        40.68433, -74.39967,
    },
    "Google": Vertex{
        37.42202, -122.08408,
    },
}
```

- 修改映射 `m[key] = elem`
- 获取元素 `elem = m[key]`
- 删除元素 `delete(m, key)`
- 检测某个键是否存在 `elem, ok := m[key]`
  - 若`key`在映射中，`ok`为 `true`；否则，`ok`为`false`。
  - 若`key`不在映射中，那么`elem`是该映射元素类型的零值。