# Java笔记

## 基本概念

- Java使用引用来操作对象。Java使用垃圾回收器来监视使用`new`创建的所有对象，辨明不再需要的对象，随后释放这些对象的内存空间。
- Java类中的数据成员称为“字段”，成员函数称为“方法”。

## 代码组织

- 每个`.java`文件是一个编译单元；一个编译单元中可以有多个类，但最多只有一个public类。当编译单元中存在public类时，编译单元的文件名需与public类类名保持一致；否则，文件名与编译单元内任意类名相同即可。
- 使用命令行编译时，只需要指定编译入口类，编译器会自动编译所需的类。

## 数据类型

- boolean(Boolean), char(Character)
- byte(Byte), short(Short), int(Integer), long(Long)
  - `Type.MAX_VALUE`, `Type.MIN_VALUE`
- float(Float), double(Double), void(Void)
- BigInteger, BigDecimal
- 不会自动地将数值转换为Boolean值。

### 包装器方法

- Integer等 `toString()`, `toBinaryString()`
- Character `isLowerCase()`

### 字面值书写

- 整数计数法与C++形式相同，支持十进制、八进制和十六进制。
- 指数计数法与C++形式相同。

### 赋值

- 对基本类型的赋值是按值传递，对对象“赋值”时传递的是引用。
- **别名现象** 按值传递，导致传递的是引用而不是复制对象。

### 数组

不允许指定数组的大小，因为Java只持有引用。

```java
int[] arr = {... };  // 推荐，花括号初始化等价于使用new
int arr[] = {... };  // 符合C/C++习惯
```

```java
int[] arr = new int[元素个数];
```

使用花括号语法初始化对象数组

```java
Integer[] arr = {
    new Integer(1),
    new Integer(2),
    3  // 自动装箱
};
```

每种类型的数组的固有对象是`length`。

### 枚举Enum

```java
public enum Currency {
    ONE, TWO, THREE
}
```

可以在switch中使用Enum，注意枚举中的使用不需要类型限定名

```java
public class ShowCurrency {
    public static void main(String[] args)
    {
        Currency cur = Currency.ONE;
        switch(cur)
        {
        case ONE:
        case TWO:
        case THREE:
            System.out.println("This is a simple usage of Currency");
        }
    }
}
```

## 流程控制

Java中`if-else`, `while`, `do-while`, `for`, `switch`形式上与C++保持一致。

注意Java中的逗号操作符只在`for`中使用。

Java中的`foreach`与C++保持一致，形式上是`for (char c : string)`

### “goto”与标签

Java中没有`goto`，但把`break`和`continue`结合标签使用

```java
label1:
outer-iteration {
    // ...
    inner-iteration {
        // ...
        break;            // 跳出内层循环
        continue;         // 内层循环重新开始
        continue label1;  // 从外层循环重新开始
        break lable1;     // 结束外层循环
    }
}
```

合理利用可以减少flag的传递。

### `foreach`

```java
for (Type value : values) {
    // 循环体
}
```

## 类

### 初始化

- **静态初始化** Java为类的基本数据成员提供默认的初始化，Java保证必要的初始化必须进行。
- **指定初始化** 在声明类成员处赋值。

可以使用`static`块组织静态初始化的代码：

```java
static int i;
static {
    i = 12;
}
```

### 构造器

基本内容与C++保持一致。

### 清理：终结处理和垃圾回收

Java中的`finalize()`方法会在对象被回收之前调用。

仅仅使用`finalize()`应对类似C语言的内存分配的清理工作，或者进行对象回收的“终结条件”验证。

使用`System.gc()`执行垃圾回收。

#### 垃圾清理概要

- 引用计数与堆栈或静态储存区追溯
- “停止-赋值”、“标记-清理”
- JIT(Just in time), lazy evalution

### 方法

#### 可变参数列表

可变参数列表可以接受0个参数。

数组形式

```java
void func(Object[] objs) {
    for (Object obj : objs) {
        // ...
    }
}
```

省略号语法

```java
void func(Object... objs) {
    for (Object obj : objs) {
        // ...
    }
}
```

由于可变参数列表可以接受0个参数，Java中存在自动装箱机制，因此重载方法接受基本数据类型时可能遇到因为0个参数而无法判定调用哪个重载方法的问题。

## 常用类

### java.util.Arrays

- `Arrays.toString()` 打印数组

### java.util.Random

```java
Random rand = new Random(47);
rand.nextInt(100);  // [0, 100) 左闭右开
```

## 访问权限控制

- Java没有条件编译，但可以通过import发行包和调试包来实现类似的功能

### 访问权限修饰词

- `public` **接口访问权限**
- 无修饰词为**包访问权限**
- `protected` **继承访问权限**
- `private` **封闭的访问权限**

## 复用类（组合、继承与代理）

### `final`关键字

### 继承

- 先构建基类部分，再构建子类部分。
- 在子类的构造器中初始化子类的代码之前，使用`super()`调用基类的构造器。

### final数据

- static final 编译器常量
- final 运行期常量
- final参数 方法中不可改变参数

### final方法

- 禁用重载

### final类

- 禁止继承

## 多态

## 常见问题处理方式

### 数字格式

`java.text.NumberFormat`, `java.text.DecimalFormat`

每三位数字插入一个分隔符

```java
NumberFormat formatter = new DecimalFormat(",###");
formatter.format(number)
```
