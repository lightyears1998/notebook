# Java 模块

## 包`package`

Java使用包来组织类。

运行有包名的主类时必须使用完全限定名称。

```sh
javac package/name/*.java
java package.name.MainClass
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
