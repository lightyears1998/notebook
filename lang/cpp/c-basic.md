# C语言笔记：基础

## 自动类型转换

自动类型转换的规则如下：

- 在表达式里，`char`和`short`类型自动转换为`int`，需要时转换为`unsigned int`。
- 在传递给`printf("%f")`时，`float`自动转换为`double`。
- 在包含两种数据类型的运算中，两个值被转换成两种类型里较高级的类型。
- 在赋值语句中，计算的最后结果被转换成被赋值的变量的类型（可能导致降级）。

## 控制语句：循环

### while循环

`while (expression) statement;`

*statement*部分既可以是带有分号的简单语句，也可以是使用花括号包围的一个复杂语句，也可以是一条空语句。

只有*expression*为真，*statement*才会执行。

空语句示例：

```c
while( scanf("%d", &num) == 1 )
    // 跳过整数输入
;
```

### for循环

`for(ctrl_1; ctrl_2; ctrl_3) statement;`

控制表达式1在循环开始前执行；控制表达式2为真时开始一次迭代；控制表达式3在一次迭代完成后执行。

### do while循环

`do statement while(expression);`

### 循环辅助手段

- `continue` 循环的其余部分被忽略，开始下一次循环；对于for循环，从控制段的更新部分开始；对于while循环，从判断循环表达式开始。
- `break` 跳出一层循环；对于for循环，不执行控制段的更新部分。

## 分支和跳转

### `if... else...`

`if(epression) statement`

`if(expression) statement1 else statement2`

`if(expression1) staement1 else if(expression2) statement2 else statement3`

### 多重选择 switch

```cpp

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

case标签必须为整型。如果没有break标签，匹配标签之后的语句都会被执行，直到遇到break标签或switch结构结束。

### `goto`

- `label: statement`
- `goto label;`

## 函数

### 函数原型

`retrun-type function-name(arguments-list);`

函数原型中函数的参数可以省略变量名。

### 形式参数与实际参数

函数定义中头部的参数是形式参数，函数调用时使用的参数是实际参数。实参复制给形参。实参与形参相互独立。

### 函数声明

函数可以在全局声明也可以在函数中声明。在函数中声明的函数在全局有效。函数在调用前需要先声明。

函数可以声明为无参数或不确定参数。

### 递归

函数可以递归调用。在return语句之前的递归称为尾递归。

## 数组和指针

### 数组

声明和初始化：

`type identifer[N] = {elem1, elem2, ..., elemN};`

`N`可被省略，编译器将根据指定元素的个数初始化数组；部分初始化数组，数组其余元素会被自动初始化为0。

使用`{[1]=elem1, ..., elemN}`语法来指定初始化。如果指定初始化元素后有更多元素，则它们被用于后续数组元素的初始化。如果多次对一个元素初始化，最后一次有效。

使用花括号对数组初始化的语法仅在数组声明时有效。不能将数组作为一个整体进行赋值。

#### 多维数组

`type identifier[X][Y];`

*identifier* 是一个由x个元素组成的数组，而它的每一个元素是y个type类型元素组成的数组。

可以使用花括号语法声明和初始化数组：

```c
type identifier[X][Y] = {
    {elem11, elem12, elem13, ..., elem1y},
    {elem21, elem22, elem23, ..., elem2y},
    ...,
    {elemx1, elemx2, elemx3, ..., elemxy}
}
```

使用花括号声明时也可以去掉内部的花括号，前面的元素优先得到赋值。

使用指针操作多维数组，复杂度随数组维数的增加而增加。地址的地址和指针的指针是双重间接（double indirection）的一个典型例子。

区分指针的数组和数组的指针。`int * ptr[2]`是有两个int类型指针的数组而`int (* ptr) [2]`是指向一个拥有两个int类型数据的数组的指针。方括号的结合性高于*（可以借助“靠近标识符的先结合”来判断类型）。

`ptr[2]` 是一个含有两个元素的数组 → `* ptr[2]` 是一个含有两个元素的数组，数组的元素是指针 → `int * ptr[2]` 是一个含有两个元素的数组，数组的元素是指向int类型数据的指针；

`(* ptr)` 是一个指针 → `(* ptr) [2]` 是一个指针，指向拥有两个元素的数组 → `int (* ptr) [2]` 是一个指针，指向拥有两个int类型元素的数组。

#### 声明数组参数

在声明形参时，可以使用`int ar[]`代替`int * ar`。使用这样的形式可以提示 *ar* 是指向int数组中一个元素的指针。无论怎样声明，处理数组的函数实际上是使用指针作为形式参数的。

如果不希望改变数组内容，可以用*const*修饰形参中的指向数组的指针。

声明处理多维数组的函数的形式参数，可以使用`int (* ptr) [n][x][y]`和它的等价形式`int ptr[][x][y]`（第一个方括号留空表示它是指针，如果第一个方括号没有留空，效果上等价于留空的）。

#### 变长数组（VLA）

变长数组必须是自动储存类的（也就必须在函数内部或者），不能在初始化时进行声明。

声明处理变长数组的函数，变长数组参量需要在数组之前声明。如`int sum2d(int rows, int cols, int ar[rows][cols]);`，可以省略一般形参的名称和变长数组的维数，如`int sum2d(int, int, int ar[*][*]);`

### 指针

地址运算符 &

间接运算符 *

`ptr = &bah; val = * ptr;` 等价于 `val = bah;`

使用 `type * identifier;` 来声明指针。

不要对未初始化的指针取值。

自增运算符与间接运算符存在微妙的优先级关系，试区分`*ptr++`、`*++ptr`、`*(ptr++)`、`*(++ptr)`和`(*ptr)++`。其中`*ptr++`等价于`*(ptr++)`。

使指针自增1，指针指向下一个储存单元（而不是下一个字节）。

如果指针被*const*修饰，那么指针指向的数据不应该被改变。不能把*const*指针赋给非*const*指针（这样指针指向的数据可能会改变），但可以把非*const*指针赋给*const*指针，前提是只进行一层间接运算（即被赋值的*const*指针不能是指针的指针）。

下面的例子演示了如果忽略上述前提，在双重间接的情况下*const*内容被修改的例子：

```c
const int ** pp;
int * p;
const int n = 10;

pp = &p;    // 不允许
*pp = &n;   // 使p指向n
*p = 11;    // n被修改
```

#### 基本操作

- **赋值（Assignment）** 将地址赋给指针，可以使用地址运算符或数组名。还可以使用类型指派来为不兼容的指针赋值。
- **求值（value-finding）或取值(derefering)** 使用间接运算符。
- **取指针地址** 使用地址运算符。
- **指针的整数加法和减法**
- **求差值（differencing）** 差值的单位是相应类型的大小，而不是字节。有效差值运算的前提是两个指针指向同一个数组
- **比较** 可以使用关系运算符比较两个相同类型的指针。

一个指针不能另一个指针相加或相乘。

#### 指针与数组

在表达式中使用数组名，等同于使用该数组首元素的地址，即数组名是指向首元素的（只读）指针。

指针变量和数组标识符都可以使用方括号语法和指针语法：`ar[n]`等价于`*(ar + n)`。区别在于，指针可以通过自增自减运算符（如`ar++`）来修改指向的地址，而数组名虽是指针，却是指向数组首元素的只读指针，不能被修改，即`ar++`是无效的。

### 复合文字

复合文字（Compound literal）是表示数组和结构内容的字面值。它没有标识符。

```c
(int [2]){1, 2}
```

上面的表达式创建了一个含有2个int元素的数组。表达式的值是指向数组首元素的指针。

可以省略元素的个数：

```c
(int []){1, 2, 3}
```

也适用于多维数组，但只能省略第一个维度。

```c
(int [][4]) {
    {1, 2, 3, 4},
    {5, 6, 7, 8}
}
```

可以使用复合文字初始化一个指针，或者使用复合文字作为实际参数传递给参量形式匹配的函数。

## 储存类、链接和内存管理

### 作用域

- 代码块作用域
- 函数原型作用域（如VLA）
- 函数作用域（仅适用于goto语句使用的标签）
- 文件作用域（全局变量）

### 链接

- 外部链接
- 内部链接（在外部定义中使用了储存类说明符static）
- 空连接

### 储存时期

- 静态储存时期
- 动态储存时期

自动变量不会被自动初始化。外部变量只能使用常量表达式来初始化。（只要类型不是一个数组，sizeof()就是一个常量表达式）

使用 *register* 关键字声明寄存器变量。

如果变量在其他文件声明，必须使用 *extern* 关键字来声明。

### *malloc()* 和 *free()*

`double * ptr = (double *)malloc(n * sizeof(double));` 成功分配内存则返回一个指向第一个分配内存空间的指针，否则返回空指针。应当显式地进行类型指派。

`free(ptr);` 释放占用的内存空间

*malloc()* 的等价语句是 *calloc()* 。

`double * ptr =  (double *)calloc(n, sizeof(double));` 返回值与 *malloc()* 相似。

`realloc(ptr, n * sizeof(double))` 可用于重新分配内存空间，ptr指向的空间需由`malloc`或`calloc`或者`realloc`分配，且不需要**也不能**调用`free`

### 类型限定词

#### volatile

当变量除了被程序改变之外还可能被其他代理改变时。一个变量可以同时是 *const* 和 *volatile* 。

#### restrict

只用于指针，表示该指针是访问数据块的唯一方式。

在函数原型中，参数的 *restrict* 要求保证指针是它指向的内容的唯一的访问方式。 `void * memcpy(void * restrict s1, const void * restrict s2, size_t n);` 和 `void * memmove(void * s1, const void * s2, size_t n);` *memcpy()* 要求两个位置之间不重叠， *memmove()* 允许重叠。

### static

`double stick(double ar[static 20]);`

函数原型中的 *static* 表示数组至少具有20个元素。

### 函数原型中的const和restrict

`void ofmouth(int * const a1, int * restrict a2, int n);` 的等价形式是：

`void ofmouth(int a1[const], int a2[restrict], int n);`
