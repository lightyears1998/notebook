# C# 基础

## 变量

### 命名规范

变量名大小写敏感。

- 不宜以下划线开头
- 使用驼峰风格camelCase
- 不使用匈牙利记号法则

## 基本数据类型

`int`, `float`, `double`, `decimal`, `string`, `char`, `bool`

在C#中使用以下类型同义词：

- `obejct`关键字等价于`System.Object`
- `string`等价于`String`

### 字符串插值

```cs
$"Hello, {userName.Text}"
```

### Infinity和NaN

针对于浮点数

浮点数除以0是`Infinity`

NaN参与的任何运算结果都是NaN

### 值类型和引用类型

赋值是按值传递，复制引用。

使用对象的Clone方法复制对象，必要时重载以定义“深拷贝”。

### null值和可空类型

- `null`即空引用，不能把`null`用于值类型
- 使用`?`操作符定义可空类型

```cs
int ? number = null;
if (number == null)
{
    Console.WriteLine("It is empty.");
}
```
