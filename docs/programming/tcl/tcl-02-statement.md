# TCL 语句

## 表达式

### 求值过程

1. 进行可能的[变量替换](#变量替换)。
2. 对剩余部分求值。

### 变量替换

- `$varName` 被替换为变量实际的值。
- `[ expression ]` 中括号表达式的值被替换为中括号内的命令执行后的返回值。

### 数值计算 `expr args...`

- 使用 `{ }` 闭合参数列表比不适用花括号更快也更安全。

``` tcl
% set userinput {[puts DANGER!]}
[puts DANGER!]
% expr $userinput == 1
DANGER!
0
% expr {$userinput == 1}
0
```

### `incr`

`incr varName ?increment?`

使数值变量自增。

## 分支语句 `if`

``` tcl
if {expr1} ?then? {
    body1
} elseif {expr2} ?then? {
    body2
} elseif {
    ...
} else {
    bodyN
}
```

## 分支语句 `switch`

``` tcl
switch ?options? string {
    pattern1 {
        body1
    }
    ?pattern2 {
        body2
    }?
    ...
    ?patternN {
        bodyN
    }?
}
```

较少使用的替代语法（可能在 switch 的语句是由变量替换得来的时候较为有用。）

``` tcl
switch ?options? string\
    pattern1 {
        body1
    }\
    ?pattern2 {
        body2
    }?\
    ...\
    ?patternN {
        bodyN
    }?
```

- 如果最后一个 pattern 是 default，则这个分支会被执行。
- `?options?` 可以指定为 `-exact` `-glob` 或 `-regexp`

## 循环语句 `while`

``` tcl
set x 0
while {$x < 5} {
    puts "x is $x"
    set x [expr {$x + 1}]
}
```

- TCL 中一切都是命令，一切命令都要经过变量替换；因此 while 循环的测试语句必须被 {...} 包围（使得变量替换在 while 命令内部发生而不是在对 while 的参数求值时发生）；若使用双引号，则变量替换只发生一次，可能导致死循环。

## 循环语句 `for`

`for start test next body`

## 循环语句 `foreach`

见[TCL List](tcl-04-util.md#List)。
