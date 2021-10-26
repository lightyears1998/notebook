# PHP 语句

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
