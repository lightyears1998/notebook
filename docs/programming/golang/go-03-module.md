# Go 模块

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
