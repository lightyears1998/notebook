# PHP 语句

## 变量

`var_dump()`, `var_export()`

- 区分大小写；
- 以美元符号开头；
- 标识符由字母数字或下划线组成，不能以数字开头。

变量在声明时不需要附加类型信息。

### 可变变量

变量的变量名可以动态地设置和使用。

```php
$a = 'hello';
$$a = 'world';
echo $a;        // 输出hello
echo $$a;       // 输出world
echo $hello;    // 输出world
```

超全局变量和 `$this` 不能用作可变变量。

### 引用赋值 `&`

``` php
$foo = 'Bob';              // 将 'Bob' 赋给 $foo
$bar = &$foo;              // 通过 $bar 引用 $foo
$bar = "My name is $bar";  // 修改 $bar 变量
echo $bar;
echo $foo;                 // $foo 的值也被修改
```

只有具名变量才能使用引用赋值。

``` php
$bar = &(1);  // 非法
```

### 作用域

变量的作用域会延伸至其后 `include` 或 `require` 的变量中。

## 常量

- `define('NAME', 'PHP');` 定义NAME为字符串常量“PHP”
- `const NAME='PHP';` 使用 `const` 定义常量时，只能在文件的最顶端定义而不能在函数内、循环或 if 语句内定义。

辨析：

- 常量的标识符前没有美元符号;
- 常量不理会变量的作用域，定义之后可以在任何地方访问;
- 常量一旦定义就不可以取消定义或重新定义;
- 常量的值只能是标量。

### 常量的工具方法

- `definded(常量名字符串)` 检查某常量是否存在

### 内置常量

- `__DIR__`, `__FILE__`, `__LINE__`
- `__FUNCTION__`, `__CLASS__`, `__TRAIT__`, `__METHOD__`, `__NAMESPACE__`
- `PHP_VERSION`, `PHP_OS`
- `TRUE`, `FALSE`

## 运算符

- 赋值 `=` 赋值总是按值传递
- 引用赋值 `$a = &$b`
- 三元运算 `? :`
- NULL合并运算符，简化`isset()` `$name = $_GET['name'] ?? false` 不存在时返回`false`，否则返回`$_GET['name']`
- 太空船操作符（结合比较运算符） `$a <=> $b` 当`$a`分别小于、等于或大于`$b`时，分别返回-1, 0或1，比较的规则沿用PHP常规比较规则

### 比较运算符

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

### 逻辑运算符

`!`, `&&`, `||`, `and`, `or`

### 错误控制运算符 `@`

```php
@mkdir('dir_name');  // 即使出现错误也会继续执行下去
```

### 执行运算符

``` php
$output = `ls -al`;
echo "<pre>$output</pre>";
```

等同于 `shell_exec()`，在激活安全模式或关闭 `shell_exec()` 时无效。

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

### 流程控制的替代语法

PHP 提供了一些流程控制的替代语法，包括 if，while，for，foreach 和 switch。替代语法的基本形式是把左花括号（{）换成冒号（:），把右花括号（}）分别换成 endif;，endwhile;，endfor;，endforeach; 以及 endswitch;。

``` php
<?php if ($a == 5): ?>
A is equal to 5
<?php endif; ?>
```

### `declare`

详见[PHP手册：Declare](https://www.php.net/manual/zh/control-structures.declare.php)
