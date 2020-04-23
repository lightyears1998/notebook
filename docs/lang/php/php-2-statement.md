# PHP语句

## 变量声明

- 区分大小写；
- 以美元符号开头；
- 标识符由字母数字或下划线组成，不能以数字开头。

变量在声明时不需要附加类型信息。

### 可变变量

变量的变量名可以动态地设置和使用

```php
$a = 'hello';
$$a = 'world';
echo $a;        // 输出hello
echo $$a;       // 输出world
echo $hello;    // 输出world
```

### 常量定义

有两种方式定义常量

- `define('NAME', 'PHP');` 定义NAME为字符串常量“PHP”
- `const NAME='PHP';`

辨析

- 常量的标识符前没有美元符号
- 常量不理会变量的作用域，定义之后可以在任何地方访问
- 常量一旦定义就不可以取消定义或重新定义
- 常量的值只能是标量

工具方法

- `definded(常量名字符串)` 检查某常量是否存在

内置常量

- `__DIR__`
- `__FILE__`
- `__LINE__`
- `PHP_VERSION`, `PHP_OS`
- `TRUE`, `FALSE`

### 运算符

- 赋值 `=` 赋值总是按值传递
- 引用赋值 `$a = &$b`
- 三元运算 `? :`
- NULL合并运算符，简化`isset()` `$name = $_GET['name'] ?? false` 不存在时返回`false`，否则返回`$_GET['name']`
- 太空船操作符（组合比较符） `$a <=> $b` 当`$a`分别小于、等于或大于`$b`时，分别返回-1, 0或1，比较的规则沿用PHP常规比较规则

慎用比较

- `!=` `<>` 数据类型转换后不相等
- `==` 数据类型转换后相等
- `===` 数据类型及值全等
- `!==`

```php
$a = 1;
$b = '1 test';
echo $a == $b;  // 返回TRUE
echo $a === $b;  // 返回FALSE，不产生输出
```

逻辑运算符

`&&`, `AND`, `||`, `OR`, `!`, `NOT`

`&&`比`AND`优先级高，以此类推。

错误控制运算符 `@`

```php
@mkdir('dir_name');  // 即使出现错误也会继续执行下去
```

## 流程控制

```php
if (exp)
else if (exp)
elseif (exp)
```

```php
switch(exp) {
    case 1:
    case 2: break;
    default:
}
```

```php
while (exp) {
    // body
}

do {
    // body
} while (exp);
```

```php
for (exp1; exp2; exp3) {
    // body
}
```

```php
foreach($数组 as $数组元素) {
    // body
}

foreach($数组 as $键值 => $元素值) {
    // body
}
```
