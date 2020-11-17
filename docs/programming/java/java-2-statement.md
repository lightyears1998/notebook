# Java语句

## 表达式

### 赋值

- 对基本类型的赋值是按值传递，对对象“赋值”时传递的是引用。
- **别名现象** 按值传递，导致传递的是引用而不是复制对象。

## 分支和循环语句

Java中`if-else`, `while`, `do-while`, `for`, `switch`形式上与C++保持一致。

注意Java中的逗号操作符只在`for`中使用。

Java中的`foreach`与C++保持一致，形式上是`for (char c : string)`

### “goto”与标签

Java中没有`goto`，但把`break`和`continue`结合标签使用。

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
