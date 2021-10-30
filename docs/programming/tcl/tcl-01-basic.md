# TCL 基础

## 注释

1. 整行注释
2. 以 # 起首的行末注释（前一个语句需要以分号结尾）

## 变量

- `set varName ?value?`
- `set varName(index) ?value?` 关联数组形式
- `unset varName`

### 作用域操纵 `upvar` `global`

`upvar ?level? otherVar1 myVar1 ?otherVar2 myVar2? ...`\
`global varName ...`

- `upvar` 用于将其他作用域的**变量** `otherVar` 绑定到当前作用域的**变量名** `myVar` 上。注意是将变量绑定到变量名上，而不是将变量名绑定到变量名上。
- `level` 默认是1。
- `level` 如果是数字，那么则是往调用栈上数的层数。
- `level` 如果是前导# + 数字，则是从 global 往下数的层数。
- `global` 相当于 `level #0 varName varName`。

``` tcl
proc SetPositive {variable value } {
    upvar 1 $variable myvar
    if {$value < 0} {
        set myvar [expr {-$value}]
    } else {
        set myvar $value
    }
    return $myvar

    # Or more concisely:
    # set myvar [expr {abs($myvar)}]
}

SetPositive x 5
SetPositive y -5

puts "X : $x    Y: $y\n"
# X : 5    Y: 5
```

## 基本数据类型

### 字符串

实际上，在 TCL 里，一切都可以表达成字符串的形式！

- 对于以空白字符界定的输入，每个输入不是命令就是字符串参数。
- `"双引号字符串"` 允许使用[变量替换](tcl-02-statement.md#变量替换)。
- `{花括号字符串}` 不允许变量替换。（注意到尽管在这层不允许变量替换，但若有多层花括号、中括号、双引号的嵌套，则里面的变量还是有可能进行变量替换的。）

#### 字符跳脱

``` tcl
"This string comes out\
on a single line"; # out 后会被添加一个空格。
```

### `expr`操作数：整数

- 十进制数
- `0b...` 二进制数
- `0o...` 或 `0...` 八进制数

### `expr`操作数：浮点数

- `xxx.yy`
- `x.`
- `.yy`
- `xxEyy`
- `xx.yye+zzz`

### `expr`操作数：布尔值

- `1` 或 `0`
- `true` 或 `false`
- `yes` 或 `no`
- `on` 或 `off`

### `expr`操作数的类型转换

``` tcl
double int wide entier
```

## 复合数据类型

### List

TCL 其实就是 List 处理器。List 相当于图灵机的“无限长的纸带”。

- 一切都是字符串，而一个由空格隔开的字符串就是一个 List。
- List 可以嵌套。

#### List 语法

- `list ?arg1? ?arg2? ... ?argN?`
- `split string ?splitChars?`
- `lindex list index` 返回列表中的第 index 个元素
- `llength list` 返回列表长度

#### List 的 Foreach 语法

`foreach varName list body` 相当实用。

``` tcl
# 一次性取得多个元素。
foreach {a b} $listofpairs { ... }

# 从不同列表中取得元素
foreach a $listOfA b $listOfB {
    ...
}
```

#### List 的元素操纵命令

- `concat ?arg1 arg2 ... argn?` 若参数是一个列表，则展开列表的内容参与拼接（对于嵌套列表，只会展开一层。）
- `lappend varName ?arg1 arg2 ... argn?`
- `linsert listValue index arg1 ?arg2 ... argn?`
  - index 可以是 end 或大于等于列表长度，此时相当于 `lappend`
- `lreplace listValue first last ?arg1 ... argn?`
- `lset varName index newValue`
- `lassign list ?varName ...?` 将 list 的元素展开赋值给各个 varName，类似于一次性取得多个元素的 foreach。

#### List 的搜索和区间命令

- `lsearch ?options? list pattern`
- `lsort ?options? list` 异地排序
- `lrange list first last` 取闭区间 [first, last]

``` tcl
# 自定义命令的搜索
proc sort {a b} {
    return [expr {[lindex $a 0] - [lindex $b 0]}]
}

for {gets stdin T} {$T} {incr T -1} {
    lassign [gets stdin] S_A S_B S_C
    set questions "{{$S_A} Draw} {{$S_B} Bob} {{$S_C} Alice}"
    set questions [lsort -command sort $questions]
    puts [lindex $questions 0 1]
}

```

### 关联数组

关联数组实质是一个哈希表。

``` tcl
set name(first) "Mary"
set name(last)  "Poppins"

puts "Full name: $name(first) $name(last)"
```

- `array exists arrayName`
- `array names arrayName` 返回关联数组中的键。
- `array size arrayName` 返回关联数组的大小。
- `array get arrayName` 返回关联数组的键值对的列表。
- `array set arrayName dataList` 将列表转换为关联数组。
- `array unset arrayName ?pattern?`

元素操纵

- `parray arrayName`

### Dict

Dict 类似于 List，但以一种更高效的方式处理键值对。并且 Dict 是纯粹的值，可以直接传递给过程，而不需要像 List 那样“通过引用传参”。

- `dict set dictVarName keyFirst ?keySecond? ?... keyNth? value` Dict 允许多重嵌套。
- `dict for {key value} $dictVarName { ... }` 类似于用于 List 的 foreach，在多重嵌套时只展开最外面的一层。
- `dict with dictVarName { ... $key1 ... $key2 ... }` 将 dictVarName 的 key 解包对对应名称的本地变量上。
- `dict get $dictVarName`
- `dict keys $dictVarName`
