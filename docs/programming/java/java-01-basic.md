# Java 基础

## 基本数据类型

基本数据类型与它对应的包装器：

- `boolean`(`Boolean`), `char`(`Character`)
- `byte`(`Byte`), `short`(`Short`), `int`(`Integer`), long(`Long`)
  - `Type.MAX_VALUE`, `Type.MIN_VALUE`
  - `Type(Type num)`, `Type.typeValue()`
- `float`(`Float`), `double`(`Double`), `void`(`Void`)
- `BigInteger`, `BigDecimal`
- 不会自动地将数值转换为`Boolean`值。

处理较大数据时使用的：`BigInteger`, `BigDecimal`。

### 包装器方法

- Integer等 `toString()`, `toBinaryString()`
- Character `isLowerCase()`

### 字面值书写

- 整数计数法与C++形式相同，支持十进制、八进制和十六进制。
- 指数计数法与C++形式相同。

## 复合数据类型

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
