# Groovy笔记

Apache基金会下Java平台的脚本语言。

## 语法特色

- 分号可以省略
- 括号在不产生歧义时可以省略，如`print 1 + 10`
- Groovy没有Java中的`Primitive type`，所有原始类型都使用对应包装类
- 使用`def var`或`Typename var`来定义变量；类型明确的前提下可以省略`def`或`Typename`
- 自动导入以下包和类型
    1. java.lang, java.util, java.io, java.net
    2. groovy.lang, groovy.util
    3. java.math.BigInteger, Java.math.BigDecimal

## 基本数据类型

原始类型全部使用对应包装器。

注意在Groovy中可以使用单引号定义字符串，使用双引号定义插值字符串。

```groovy
assert 3.class == Integer
assert (3.5).class = BigDecimal
assert 'abc' instanceof String
assert "abc" instanceof String

String name = 'Dolly'
assert "Hello, ${name}!" == 'Hello, Dolly!'  // 字符串插值完整形式
assert "Hello, $name" == 'Hello, Dolly!'     // 字符串插值无歧义时的简短形式
assert "Hello, $name" instanceof GString
```

### 静态数据类型和动态数据类型

```groovy
Integer n = 3
Date now = new Date()

def x = 3
assert x.class = Integer
x = 'abc'
assert x.class = String
x = new Date()
assert x.class = Date
```

### Groovy真值

- 非0数字是真
- 非空集合是真
- 非null引用是真
- Boolean类型的true是真

### 操作符重载

- 求幂运算 `**`
- String的操作符重载 `-`

### 集合Set

- 定义集合 `` ArrayList
- 转换集合 `` `as`用于转换兼容集合

```groovy
def nums = [1, 1, 2, 3, 5]  // java.util.ArrayList
Set uniques = nums as Set   // `as`用于进行兼容转换
```

### 映射Map

```groovy
def map = [a:1, b:2, c:3]

map.a
map['b']
map.get('c')
```

## 闭包

### `each`方法

```groovy
def nums = [1, 2, 3, 4, 5]
def doubles = []

nums.each { n ->  // 箭头操作符
    doubles << n * 2
}

assert doubles == [2, 4, 6, 8, 10]
```

### `collect`方法

```groovy
def nums = [1, 2, 3, 4, 5]
def doubles = nums.collect { it * 2 }
assert doubles == [2, 4, 6, 8, 10]
```

---

## 安装

在Windows平台上访问[官网下载](https://groovy.apache.org/download.html)页面。
