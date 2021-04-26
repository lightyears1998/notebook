# Groovy 基础

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

### Groovy提供的操作符重载

- 求幂运算 `**`
- String的操作符重载 `-`
