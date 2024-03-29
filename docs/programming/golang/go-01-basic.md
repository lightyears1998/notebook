# Go 基础

## 变量

### 变量声明

1. `var`可用于声明变量；简洁赋值语句`:=`可在类型明确时代替`var`，但只能在函数内使用。（在函数外的语句只能由关键字起首。）
2. 没有明确初始值的变量会自动被赋予零值。
3. 类型名在变量名之后，如果多个变量类型相同，则除最后一个外，其他类型说明可以省略。
4. `fmt.Printf("类型名：%T，值：%v", variable, variable)`

### 常量声明

1. 常量使用`const`声明，不能使用简洁赋值语句来声明常量。
2. 常量由上下文来决定具体类型。（数值常量总是高精度的值。）

## 基本数据类型

- 与C语言不同，Go在不同数据类型的项之间赋值需要显式类型转换，即使不会发生截断。

### 指针

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
for i, v := range pow {
    fmt.Printf("2**%d == %d", i, v)
}
```

## 映射

映射将键映射到值。

```go
m := make(map[string]Vertex)

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
- 键的数量 `len(m)`
- 删除元素 `delete(m, key)`
- 检测某个键是否存在 `elem, ok := m[key]`
  - 若`key`在映射中，`ok`为 `true`；否则，`ok`为`false`。
  - 若`key`不在映射中，那么`elem`是该映射元素类型的零值。
