# PHP 基础

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

## 输出标签

``` php
<?php expression; ?>
<?= expression ?>
```

``` php
#!/usr/bin/env php
<?php
```

``` php
<?php if ($expression == TRUE): ?>
  This will show if the expression is TRUE.
<?php else: ?>
  Otherwise this will show.
<?php endif; ?>
```

- 尽量不要使用短标记；使用 `--enable-short-tags` 启用短标记`<? ... ?>`。
- 使用分号作为语句分隔符 `;`。

### 作用域

变量的作用域会延伸至其后 `include` 或 `require` 的变量中。


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

## 语言结构

### `echo`

``` php
echo 'Hello, world!', PHP_EOL
```

## 注释

PHP 支持三种风格的注释。

```php
# Life is like a box of chocolate.

// Life is like a box of chocolate.

/**
 * Life is like a box of chocolate.
**/
```

## 数据类型

PHP 的数据类型在运行时动态地决定，共有 9 种原始数据类型。

- 四种标量类型：布尔型（`boolean`），整型（`integer`），浮点型（`float`，关键字 `double` 已弃用），字符串型（`string`）
- 三种复合类型：数组（`array`），对象（`object`）、可调用（`callable`）
- 两种特殊类型：资源（`resource`），无类型（`NULL`）

在文档和注释常用的伪类型：`mixed`（混合类型）、`number`（数字）、`callback`、`array` | `object` 和 `void` 类型。

### 数据类型的工具函数

- `vardump(expr)` 查看表达式 `expr` 的类型和值。
- `print_r(expr)` 打印基本或复合数据类型的值。
- `gettype(expr)` 返回表示 `expr` 类型的字符串，例如 `"string"`、`"boolean"` 等。
- `is_type` 函数族用于判断变量的类型。

### 类型转换

- 临时强制转换 `(type)$var`
- 持久强制转换 `settype($var, 'int')`

另可参见[类型转换的判别](https://www.php.net/manual/zh/language.types.type-juggling.php)和[类型比较表](https://www.php.net/manual/zh/types.comparisons.php)。

## 标量类型（基本数据类型）

### 布尔型

`boolval()`, `is_bool()`, `settype($var, "boolean")`, `setttype($var, "bool")`

- 值取 `TRUE` 或 `FALSE`，不区分大小写。
- 使用 `echo` 输出时，`TRUE` 输出 1，`FALSE` 输出空字符串。

#### 转换为布尔类型

在进行类型转换时，被转换为 `FALSE` 的值有：

- `FALSE` 本身；
- 整型 `0` 以及浮点数 `0.0`；
- 空字符串 `""` 以及字符串 `"0"`；
- 空数组；
- `NULL` 以及尚未赋值的变量；
- 从空标记生成的 SimpleXML 对象。

任何其他值都被认为是TRUE。注意一切 Resource 被转换为 `TRUE`。

### 整型

`intval()`, 乘方`**`

取值范围在 `PHP_INT_MIN` 和 `PHP_INT_MAX`之间。

```php
$num = 1234;
$num = 0234;  // 八进制
$num = 0x34;  // 十六进制
$num = 0b11111111; // 二进制
```

另参见[PHP 数学库](php-library/math.md)

#### 转换为整型

1. `TRUE` => `1`, `FALSE` => `0`;
2. 浮点数向下取值；`NaN` => `0`；`Infinity` => `0`；
3. 见[字符串转换为数值](#字符串转换为数值)
4. 未定义从其他类型转换为整型的行为。

### 浮点型 float

`floatval()`

``` php
$num = 1.234;
$num = 1.2e3;
$num = 7E-10;
```

#### `NaN`

`is_nan()`

- 不要使用 `==` 或 `===` 比较 `NaN`；使用 `is_nan()` 来检查 `NaN`。

#### `Infinity`

`is_infinite()`

#### 转换为浮点型

类似于整型。

### 字符串 string

`strval()`

- 每个字符等同以一个字节（因此不支持 Unicode），最大可达 2 GiB；
- 字符串的连接使用 `.` 操作符而不是 `+`。
- 成员访问使用中括号或花括号 `$str[42]` `$str{42}`。（注意避免在多字节字符集中使用中括号语法访问成员）

PHP 中的 string 的实现方式是一个由字节组成的数组再加上一个整数指明缓冲区长度。并无如何将字节转换成字符的信息，由程序员来决定。字符串由什么值来组成并无限制；特别的，其值为 0（“NUL bytes”）的字节可以处于字符串任何位置（不过有几个函数，在本手册中被称为非“二进制安全”的，也许会把 NUL 字节之后的数据全都忽略）。

#### 单引号字符串

字符串中的变量和特殊字符的转义序列不会被展开。
（如 `\n` 和 `\t` 等均不展开，但 `\'` 和 `\\` 除外。）

#### 双引号字符串

用双引号定义的字符串，其中的变量会被解析，并且转义特殊字符。

```php
$hel = 'hel';
echo "$hel lo"  // 可解析
echo "$hello"   // 不可解析，提示未定义变量
```

#### Heredoc 语法结构

```php
<<<EOT
多行字符串
EOT

// EOT 无引号包围，如同使用双引号包围
// 注意最后的 EOT 标记必须单独成一行，即没有缩进，其后也没有其他字符
```

heredoc 会对其中变量解析并且转义特殊字符。

```php
$a = 'test'
$str = <<<EOD
a = $a\n
EOD;
echo $str;  // 输出test并附加换行符
```

#### Nowdoc 语法结构

```php
<<<'EOT'
多行字符串
EOT
```

Nowdoc 不解析变量也不转义特殊字符序列。

```php
$a = 'test'
$str = <<<'EOD'
a = $a\n
EOD;
echo $str;  // 输出 test 并附加换行符
```

#### 字符串的变量解析规则

1. 简单语法 `$name_of_variable` 遇到美元符号时尽可能的组合更多的标识符。
2. 复杂语法（花括号语法） `{$name_of_variable}`。

#### 转换为字符串

1. `TRUE` => `"1"`, `FALSE` => `""`（空字符串）；
2. 数组 => `"Array"`；
3. 对象 => `"Object"`；
4. NULL => `""`；
5. 资源 => 形如 `"Resource id #1"`。

#### 字符串转换为数值

当一个字符串被当作一个数值来取值，其结果和类型如下：

如果该字符串没有包含 '.'，'e' 或 'E' 并且其数字值在整型的范围之内（由 PHP_INT_MAX 所定义），该字符串将被当成 integer 来取值。其它所有情况下都被作为 float 来取值。

该字符串的开始部分决定了它的值。如果该字符串以合法的数值开始，则使用该数值。否则其值为 0（零）。合法数值由可选的正负号，后面跟着一个或多个数字（可能有小数点），再跟着可选的指数部分。指数部分由 'e' 或 'E' 后面跟着一个或多个数字构成。

## 复合数据类型

### 数组

数组即有序映射，key 是 integer 或 string 类型，value 可以是任意类型。（因此支持多维数组。）

- 定义数组 `array({"a"=>"apple", "b"=>"banana"});` 短定义语法 `['a'=>1, 'b'=>2]`
- 使用中括号语法或花括号语法访问数组元素 `array[key]`, `array{key}`
- 打印数组 `var_dump()`, `print_r()`
- 数字索引和关联索引可以同时存在。（混合索引数组。）

#### key 的强制类型转换

- 包含有合法整型值的字符串会被转换为整型。例如键名 "8" 实际会被储存为 8。但是 "08" 则不会强制转换，因为其不是一个合法的十进制数值。
- 浮点数也会被转换为整型，意味着其小数部分会被舍去。例如键名 8.7 实际会被储存为 8。
- 布尔值也会被转换成整型。即键名 true 实际会被储存为 1 而键名 false 会被储存为 0。
- `Null` 会被转换为空字符串，即键名 `null` 实际会被储存为 ""。
- 数组和对象不能被用为键名。坚持这么做会导致警告：Illegal offset type。

必须小心 key 的覆盖问题：若数组定义时多个单元使用同一个键名，那么最后一个单元之前的内容均会被覆盖。

#### 自动设置键名

PHP 可以自动设置键名或仅对一些单元指定键名。

```php
$food = array("饼干", "巧克力", "蛋糕");  // 键名分别为 0，1，2
$food[] = "瓜子";  // 设置键名为 3
```

#### 数组指针

数组中有内部指针，指向当前的元素。foreach 不会移动数组内部指针。

`current()`, `each()`以数字索引数组和关联索引数组形式返回键名和键值，并移动, `end()`, `next()`, `prev()`

#### 数组运算符

- `+` 把右边的数组元素附加到左边的数组后面，两个数组中都有的键名，则只用左边数组中的，右边的被忽略；
- `==` 如果 $a 和 $b 具有相同的键／值对则为 TRUE；
- `===` 如果 $a 和 $b 具有相同的键／值对并且顺序和类型都相同则为 TRUE。

#### 数组类型的工具函数

- `count(array [, mode])` 计算数组中元素的个数，mode=1时递归统计多维数组的元素
- 数字索引数组排序 `sort(array, [, sortingtype])`, `rsort()` 可设定多种排序类型
- 关联索引数组键值排序 `asort()`, `arsort()` 保持键值对，按值进行排序
- 关联索引数组键名排序 `ksort()`, `krsort()` 保持键值对，按键名排序
- 添加元素 `array_push()` 向末尾追加元素 `array_unshift()` 向开头添加元素，往弹夹里压子弹
- 删除元素 `array_pop()`, `array_shift()`
- 删除重复元素，即使键名不同 `array_unique()`
- 查询数组元素 `in_array()`
- 返回键名/键值数组 `array_keys()`, `array_values()`
- 删除数组中的元素 `unset($array[key])`
- 统计数组中的值出现的次数 `array_count_values($array)`

#### 转换为数组

1. 标量类型和 Resource 类型转换为仅有一个元素的数组，key 为 0，值为标量的值。即 `(array)$scalar === array($scalar)`。
2. `NULL => 空数组`
3. 如果一个 object 类型转换为 array，则结果为一个数组，其单元为该对象的属性。键名将为成员变量名，不过有几点例外：整数属性不可访问；私有变量前会加上类名作前缀；保护变量前会加上一个 '*' 做前缀。这些前缀的前后都各有一个 NULL 字符。

### 对象

`new`, `get_class()`

#### `instanceof` 操作符

确定一个变量是否为某个类或接口的实例。子类是继承父类的实例。

``` php
class SomeClass {}
$a = new SomeClass;
$b = new SomeClass;

var_dump($a instanceof SomeClass);    // true
var_dump($a instanceof "SomeClass");  // true
var_dump($a instanceof $b);           // true
```

## 特殊类型

### 资源 Resource

保存到外部资源的一种引用。

`$handle = fopen($filename, $filemode);`

### 无类型 `Null`

`is_null`, `unset`

未被赋值或被赋值为 `NULL`，或被 `unset()` 的变量是无类型的。

#### 转换到 `Null`

使用 `(unset) $var` 将一个变量转换为 `null` 将不会删除该变量或 `unset` 其值。仅是返回 `NULL` 值而已。

### Callable 类型

`call_user_func()`, `usort()`

PHP 是将函数以 string 形式传递的。 可以使用任何内置或用户自定义函数，但除了语言结构例如：`array()`，`echo`，`empty()`，`eval()`，`exit()`，`isset()`，`list()`，`print` 或 `unset()`。

使用回调函数示例：

``` php
<?php

// An example callback function
function my_callback_function() {
    echo 'hello world!';
}

// An example callback method
class MyClass {
    static function myCallbackMethod() {
        echo 'Hello World!';
    }
}

// Type 1: Simple callback
call_user_func('my_callback_function');

// Type 2: Static class method call
call_user_func(array('MyClass', 'myCallbackMethod'));

// Type 3: Object method call
$obj = new MyClass();
call_user_func(array($obj, 'myCallbackMethod'));

// Type 4: Static class method call (As of PHP 5.2.3)
call_user_func('MyClass::myCallbackMethod');

// Type 5: Relative static class method call (As of PHP 5.3.0)
class A {
    public static function who() {
        echo "A\n";
    }
}

class B extends A {
    public static function who() {
        echo "B\n";
    }
}

call_user_func(array('B', 'parent::who')); // A

// Type 6: Objects implementing __invoke can be used as callables (since PHP 5.3)
class C {
    public function __invoke($name) {
        echo 'Hello ', $name, "\n";
    }
}

$c = new C();
call_user_func($c, 'PHP!');
```

使用闭包：

``` php

<?php
// Our closure
$double = function($a) {
    return $a * 2;
};

// This is our range of numbers
$numbers = range(1, 5);

// Use the closure as a callback here to
// double the size of each element in our
// range
$new_numbers = array_map($double, $numbers);

print implode(' ', $new_numbers);
```
