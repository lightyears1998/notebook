# C语言常识

> C语言主要是由贝尔电话实验室的丹尼斯·M·里奇（Dennis M.Ritchie）开发的，从1969年开始设计并于1973年开发完成。……它是一种早期的程序设计语言B语言的后继者。B是BCPL（Basic CPL）语言的一种精简版本，而BCPL来源于CPL（Combined Programming Language）。
>
> 参见[《编码》](../books/history/《编码：隐匿在计算机软硬件背后的语言》.md)396页

- 源文件拓展名 `h`, `c`

## `main()`函数

使用`int main(void){ ... }`形式的`main()`函数。

- `void main(){}` 不符合C语言标准。
- `main(){}` 不符合C99标准。
- `int main(){}` 能编译运行，但它不是标准的C语言形式。

参见[CPP Reference网站中关于main()函数的内容](http://en.cppreference.com/w/c/language/main_function)。

## 语句

表达式（expression）由运算符和操作数组成，每个表达式都有值。一些表达式是其他表达式的组成部分，称为子表达式（subexpression）。

1. 一个（有作用的）语句（statement）是一条完整的计算机指令，语句用结束处的分号标识。C把结束处有分号的表达式看作语句，称为*表达式语句*。
2. 声明语句（declaration statement）不是一个表达式语句，它没有值。
3. 赋值语句（assignment statement）是表达式语句的一个特例。
4. 函数语句（function statement）引起函数的执行。
5. 结构化语句（structured statement）是比一般语句复杂的语句。
6. 复合语句（compound statement）或代码块（block）
7. 空语句是什么也不做的语句。

### 优先度

共享操作数的操作符，执行顺序按优先度决定；不共享操作数的操作符，即使具有同等的优先度，也不能获知哪一个运算先执行。如`7*6 + 8*9`，不知道`7*6`先执行还是`8*9`先执行。

### 副作用和顺序点

从C的角度看，C的主要目的是为表达式求值。表达式引起的数据对象的变化、文件的修改等称为副作用（side effect）。

顺序点（sequence point）是程序执行中的一点，在该点处，所有的副作用都在进入下一步前被计算。在C中，语句的分号、一些运算符、任何完整的表达式（不是子表达式的表达式）的结束标志了顺序点。
