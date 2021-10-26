# Java 工具

## 输入输出工具

### `java.util.Scanner`

```java
Scanner sc = new Scanner(System.in);
sc.hasNext(); // ...
sc.NextInt(); // ...
```

### `System.out.printf(format-string, var-list)`

类C语言的`printf`方法。

### 数字格式化工具

`java.text.NumberFormat`, `java.text.DecimalFormat`

每三位数字插入一个分隔符

```java
NumberFormat formatter = new DecimalFormat(",###");
formatter.format(number)
```

## 字符串工具

### `java.util.StringTokenizer`

## 进阶数据结构

### `java.util.Arrays`

- `Arrays.toString()` 打印数组

## `java.util.HashMap`

- `HashMap<String, Integer>`
- `size()`, `isEmpty()`
- `containsKey()`, `get()`
- `put()`
- `remove()`
