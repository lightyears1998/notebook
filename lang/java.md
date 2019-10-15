# Java笔记

## 基本概念

- Java使用引用来操作对象。Java使用垃圾回收器来监视使用`new`创建的所有对象，辨明不再需要的对象，随后释放这些对象的内存空间。
- Java类中的数据成员称为“字段”，成员函数称为“方法”。

## 代码组织

- 每个`.java`文件是一个编译单元；一个编译单元中可以有多个类，但最多只有一个public类。当编译单元中存在public类时，编译单元的文件名需与public类类名保持一致；否则，文件名与编译单元内任意类名相同即可。
- 使用命令行编译时，只需要指定编译入口类，编译器会自动编译所需的类。

## 数据类型

Java类中的数据成员称为“字段”，成员函数称为“方法”。

## Compile

- 可以使用source开关来指定目标JRE版本：`-source 1.4`

## `package`

Java使用包来组织类。

运行有包名的主类时必须使用完全限定名称。

```sh
javac package/name/*.java
java package.name.MainClass
```

## Chapter 2 数据类型

基本数据类型与它对应的包装：

- `boolean`(`Boolean`), `char`(`Character`)
- `byte`(`Byte`), `short`(`Short`), `int`(`Integer`), long(`Long`)
  - `Type.MAX_VALUE`, `Type.MIN_VALUE`
  - `Type(Type num)`, `Type.typeValue()`
- `float`(`Float`), `double`(`Double`), `void`(`Void`)
- `BigInteger`, `BigDecimal`
- 不会自动地将数值转换为`Boolean`值。

处理较大数据时使用的：`BigInteger`, `BigDecimal`

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

每种类型的数组的固有对象是`length`，代表数组的长度。

对于高维数组，形式如下：

```java
int dimTwo[][] = new int[3][4];

int dimTwo[][] = new int[3][];
dimTwo[0] = new int[1];
dimTwo[1] = new int[2];
dimTwo[3] = new int[3];
```

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

类中的静态成员也称为“类变量”。

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

### `instanceof`操作符

左边的类是否为右边的类或子类创建的对象。

## 常用类

### `java.util.Arrays`

- `Arrays.toString()` 打印数组

### `java.util.Random`

```java
Random rand = new Random(47);
rand.nextInt(100);  // 生成[0, 100)区间内的随机数
```

### `java.io.BufferedReader`

```java
public static void main(String args[]) throws IOException {
    BufferedReader br = new BufferedReader(new FileReader("ReadFile.java"));
    for (String line = br.readLine(); line != null; line = br.readLine()) {
        System.out.println(line);
    }
    br.close();
}
```

### `java.io.FileInputStream` & `java.io.FileOutputStream`

```java
FileInputStream in = new FileInputStream("CopyFile.java");
FileOutputStream out = new FileOutputStream("CopyFile.java.tmp");

int read = in.read();
while (read != -1) {
    out.write(read);
    read = in.read();
}

in.close();
out.close();
```

### `java.io.File`

```java
File[] files = new File(".").listFiles();
for (File file : files) {
    if (file.isDirectory()) {
        System.out.println("<DIR>" + file.getName());
    } else {
        System.out.println(file.getName());
    }
}
```

### `java.util.StringTokenizer`

## 访问权限控制

- Java没有条件编译，但可以通过import发行包和调试包来实现类似的功能

### 访问权限修饰词

- `public` **接口访问权限**
- 无修饰词为**包访问权限**
- `protected` **继承访问权限**
- `private` **封闭的访问权限**

## 复用类（组合、继承与代理）

### 接口 `interface`

```java
interface SomeInterface {
    // interface body
}
```

接口中的方法一定是`public abstract`。

- 若一个接口被`public`修饰，那么它可以被任何一个类实现。
- 若一个接口没有被`public`修饰，那么它可以被同一包内的类实现。

### 继承

```java
class Apple extends Fruit {
    // class definition
}

class Apple implements Etable {
    // class definition
}
```

类的继承对父类成员的访问权限符合访问权限限制，即：

1. 当子类和父类在同一个包中时，子类自然地继承父类中不是private的成员。
2. 当子类和父类在不同包中时，子类只能继承父类中public和protected的成员。

在继承中使用同名的变量时，父类同名变量隐藏，可以使用`super.var`访问。

在继承中使用同名的方法时，方法可以隐藏或重写。

对于重写，方法的类型与父类方法类型一致或者是父类方法类型的子类型。

使用`@Override`注记来指明对方法的重写。

重写父类方法时，不能降低父类方法的访问权限，这是从继承的角度看子类也是一种基类的限制。

### `abstract`关键字

```java
abstract class SomethingAbstract {
    abstract abstractMethod();

    nonAbstractMethod() {
        // function body.
    }
}
```

- abstract类可以有抽象方法和非抽象方法。
- abstract类不能使用`new`来创建对象。
- 不能同时使用abstract和final来修饰同一个类。

### `final`关键字

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

Java中的多态性是“同名不同参，同名不同义”。

## 常见问题处理方式

### 数字格式

`java.text.NumberFormat`, `java.text.DecimalFormat`

每三位数字插入一个分隔符

```java
NumberFormat formatter = new DecimalFormat(",###");
formatter.format(number)
```

## 输入输出工具

### `java.util.Scanner`

```java
Scanner sc = new Scanner(System.in);
sc.hasNext(); // ...
sc.NextInt(); // ...
```

### `System.out.printf(format-string, var-list)`

类C语言的`printf`方法。
