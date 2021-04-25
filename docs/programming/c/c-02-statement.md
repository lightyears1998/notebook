# C 语句

## 表达式语句

### 基本数学运算符

- `=` `+` `-` `*` `/` `%` `++` `--`（C中没有幂运算符）
- 整数的除法总是截尾，并且是**趋零截尾**。因此，正数的模是正数，负数的模是负数。

### 自增/自减操作符

由于不能保证在语句执行过程中何时自增，在下列情况不要使用自增/自减运算符：

- 变量多次出现在同一个表达式里
- 变量出现在同一个函数的多个参数中

### 关系运算符

- 大于（>）、小于（<）、大于或等于（>=）、小于或等于（<=）、等于（==）和不等于（!=）。
- 不能使用关系运算符比较字符串。
- 只能使用“>”或“<”来比较浮点数。
- 如果关系表达式为真，值为1；反之，值为0。
- 如果比较的双方有一方是常量，可以把常量放在左边，有助于发现错误。`5 == canoes`

### 逻辑真与假

非零为真，零为假。

### 逗号运算符

逗号运算符“,”标志了一个顺序点，保证被它分开的表达式从左到右计算。逗号表达式的值是右边成员的值。

逗号“,”也被用作分隔符。

### 与、或、非

- && 与
- || 或
- ! 非

1. 关系运算符优先级高于逻辑运算符。非运算符的优先级高于与运算符，或运算符优先级最低。
2. 与运算符和或运算符标志一个顺序点。

### 条件运算符 `?`

`expression 1 ? expression2 : expression3`

### 赋值

```c
左值 = 右值;
```

## 分支和跳转语句

### `if... else...`

```c
if (epression) statement;
if (expression) statement1; else statement2;
if (expression1) staement1; else if (expression2) statement2; else statement3;
```

### `switch`多重选择

```c
switch(integer expression)
{
    case constant1:
        statements
        break;
    case constant2:
        statements
        break;
    default:
        statements
}
```

1. `case`标签必须为整型。
2. 如果没有`break`标签，匹配标签之后的语句都会被执行，直到遇到`break`标签或`switch`结构结束。

### `goto`

```c
label:
    statement;
goto label;
```

## 循环语句

- `continue` 循环的其余部分被忽略，开始下一次循环；对于for循环，从控制段的更新部分开始；对于while循环，从判断循环表达式开始。
- `break` 跳出一层循环；对于for循环，不执行控制段的更新部分。

### `while`循环

```c
while (expression) statement;
```

### `do while`循环

```c
do statement; while(expression);
```

### `for`循环

```c
for(ctrl_1; ctrl_2; ctrl_3) statement;
```

`ctrl_1`在循环开始前执行；`ctrl_2`为真时开始一次迭代；`ctrl_3`在一次迭代完成后执行。
