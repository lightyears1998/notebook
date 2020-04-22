# C语言语句

## 赋值语句

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
