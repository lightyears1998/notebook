# C#模块

## 命名空间与程序集

1. **命名空间** `using Some::Namespace;`
2. **程序集** 类编译到程序集中，dll文件和exe文件都是程序集

注：程序集与命名空间并非一对一的关系

## 方法

### 表达式主体方法

一种语法糖

```cs
int addValue(int a, int b) => a + b;
```

### 可选参数

如同C++

### 具名参数

与Python语法稍有不同

```cs
optMethod(first: 99, second: 100, third: "101");
```

### ref参数

按引用传递，注意调用方法时也要附加`ref`关键字

```cs
static void doIncrement(ref int it) => it++;

static void Main()
{
    int arg = 12;
    doIncrement(ref arg);  // 调用方法时需要附加ref关键字
}
```

即使是ref参数也不接受未初始化的变量作为实参

### out参数

需要由参数来初始化变量时，使用out参数来初始化未初始化的变量

使用out参数后，必须在方法内部对传递的变量赋值

```cs
static void doInitialize(out int number) => number = 12;

static void Main(string[] args)
{
    int a;
    doInitialize(out a);
}
```

## 枚举

与C++不同，C#枚举不需要枚举类的语法即可拥有“类的名称空间”

```cs
enum Season {Spring, Summer, Fall, Winter};

Season local = Season.Spring;
```

## 类

类的方法默认权限为`private`

构造器、重载构造器形如Java

### Partial Class 分部类

```cs
partial class Circle
{
    // 主要功能
}

partial class Circle
{
    // 对功能的扩充
}
```

分部类不是用来将定义与实现分离的，另外C#中规定分部方法必须具有void的返回类型。

### Static Class 静态类

静态类中只能包含静态方法

### 静态using语句

将类引入作用域，使得在访问静态成员时隐藏类名，功能上Java但语法不同

```cs
using static System.Math;
using static System.Console;

var root = Sqrt(99.9);
WriteLine("");
```

### 匿名类

匿名类，没有名字的类

```cs
var anonymousObject = new { Name="John", Age = 12 };
```

编译器自动推断匿名类字段的类型，并根据字段的名称、类型、数量和声明的顺序判断两个匿名类是不是同一个类型的匿名类。

匿名类只能包含公共字段，并且不能定义方法，字段必须全部初始化，并且不能是静态的。

### is操作符

使用`is`操作符验证对象的类型

```cs
WrappedInt wi = new WrappedInt();
Object o = wi;

if (o is WrappedInt)
{
    WrappedInt tmp = (WrappedInt)o;  // 确定o是对WrappedInt的引用之后转型就是安全的
}
```

### as操作符

as操作符转换对象的类型，失败时返回`null`

```cs
WrappedInt wi = new WrappedInt();
Object o = wi;

WrappedInt tmp = o as WrappedInt;
if (tmp != null)
{
    // 只有转型成功才会执行
}
```

### System.Math

- `Sqrt()` 平方根的计算
