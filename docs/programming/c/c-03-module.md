# C 模块

单独的一个`.cpp`文件为一个编译单元。

## 函数

### 函数声明

函数可以在全局声明也可以在函数中声明。在函数中声明的函数在全局有效。函数在调用前需要先声明。

「C语言特性」函数可以声明为无参数（`void`）或不确定参数（参数列表为空）。

### 内联函数`inline`

1. 选择两者其一即可：在函数声明前附加`inline`，在函数定义前附加`inline`；
2. 可将内联函数放置于头文件中；同一个函数的所有内联定义都必须相同。

### 函数原型

```c
retrunType functionName(paremeterType parameter);
```

函数原型中函数的参数可以省略变量名。

## 头文件与实现文件

头文件与实现文件分离时，遵循**自给自足原则**和**包含防护原则**。

### 包含防护（guarding）

```cpp
#ifndef THIS_HEADER_H_
#define THIS_HEADER_H_
// 类的定义

#endif  // THIS_HEADER_H_
```

## 储存类、链接和内存管理

### 作用域

- 代码块作用域
- 函数原型作用域（如VLA）
- 函数作用域（仅适用于goto语句使用的标签）
- 文件作用域（全局变量）

### 链接

- 外部链接
- 内部链接（在外部定义中使用了储存类说明符`static`）
- 空连接

### 储存时期

- 静态储存时期
- 动态储存时期

自动变量不会被自动初始化。外部变量只能使用常量表达式来初始化。（只要类型不是一个数组，`sizeof()`就是一个常量表达式）

使用`register`关键字声明寄存器变量。

如果变量在其他文件声明，必须使用`extern`关键字来声明。

### `malloc()` 和 `free()`

`double * ptr = (double *)malloc(n * sizeof(double));` 成功分配内存则返回一个指向第一个分配内存空间的指针，否则返回空指针。应当显式地进行类型指派。

`free(ptr);` 释放占用的内存空间

`malloc()` 的等价语句是 `calloc()` 。

`double * ptr =  (double *)calloc(n, sizeof(double));` 返回值与 *malloc()* 相似。

`realloc(ptr, n * sizeof(double))` 可用于重新分配内存空间，ptr指向的空间需由`malloc`或`calloc`或者`realloc`分配，且不需要**也不能**调用`free`

### CV限定符和`restrcit`限定符

#### `const`

#### `volatile`

当变量除了被程序改变之外还可能被其他代理改变时。一个变量可以同时是 *const* 和 *volatile* 。

#### `restrict`

只用于指针，表示该指针是访问数据块的唯一方式。

在函数原型中，参数的 *restrict* 要求保证指针是它指向的内容的唯一的访问方式。 `void * memcpy(void * restrict s1, const void * restrict s2, size_t n);` 和 `void * memmove(void * s1, const void * s2, size_t n);` *memcpy()* 要求两个位置之间不重叠， *memmove()* 允许重叠。

### `static`

`double stick(double ar[static 20]);`

函数原型中的 *static* 表示数组至少具有20个元素。

### 在函数原型中CV限定符的等价形式

```c
void ofmouth(int * const a1, int * restrict a2, int n);
void ofmouth(int a1[const], int a2[restrict], int n);  // 与上一句等价。
```
