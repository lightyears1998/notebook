# PHP 模块

## 函数

- 函数只有在定义后才能被使用。
- 函数不能重载，也不能取消定义已经定义的函数。
- 函数具有全局作用域，可以在一个函数内定义而在这个函数外调用。
- 不通过 `return` 返回值的函数返回 `Null`。

### 在函数中使用全局变量

在函数中可以通过 `global` 关键字或超全局变量数组 `$_GLOBALS[]` 获取全局变量，使用 `static` 关键字定义静态变量。

```php
function foo($arg1, $arg2, $arg3, ...)
{
    return $val;
}
```

### 引用参数

```php
function foo(&$var){
    // 通过引用传递参数
}
```

### 默认参数

缺省参数只能位于函数参数表末端。

```php
<?php
function sum($c=5, $b=3, $a) {
    echo$a."+ ".$b." + ".$c." = ".($a+$b+$c);
}
sum(1);  // raise ArgumentCountError
?>
```

```php
function foo($var = 'default') {}  // 默认参数
```

### 参数类型声明

传入参数的类型错误时，PHP7抛出`Type Error`异常，PHP5报告致命错误。

可声明的参数类型：（对象或接口）`class`, `interface`, （数组）`array`, （回调函数）`callable`, （标量类型）`bool`, `int`, `string`, `float`

```php
function foo(int $var1, bool $var2, string $var3) {}
```

### 可变参数列表

使用 `...` 声明变长形式参数：

```php
function sum(...$numbers) {
    $acc = 0;
    foreach ($numbers as $n) {
        $acc += $n;
    }
    return $acc;
}

echo sum(1, 2, 3, 4);
```

使用 `...` 展开参数：

``` php
function add($a, $b) {
    return $a + $b;
}

echo add(...[1, 2])."\n";

$a = [1, 2];
echo add(...$a);
```

### 可变参数列表工具函数

- func_num_args
- func_get_arg
- func_get_args

### 返回值类型声明

```php
function foo(Type $arg) : int {}
```

### 返回引用

``` php
function &returns_reference()
{
    return $someref;
}

$newref =& returns_reference();
```

### 可变函数

```php
$functions = ['fun1', 'fun2', 'fun3'];
foreach($functions as $fun)
{
    $fun();
}
```

通过 `call_user_func($fun)` 运行回调函数。

### 匿名函数（闭包）

匿名函数是通过 Closure 类实现的。

``` php
$myfunction = function () {
    // body
};
```

闭包使用 `use` 关键字从父作用域继承变量。不能传入超全局变量、`$this` 或与其他参数重名的变量。

``` php
$variable = 'Something';

$myFunction = function () use($variable) {
    var_dump($variable);
}
```

在面向对象环境中的闭包，`$this` 是自动绑定的。如果不希望 `$this` 自动绑定，可以使用静态匿名函数。

``` php
$func = static function() {
    // function body
};
$func = $func->bindTo(new StdClass);
$func();

// Output:
// Warning: Cannot bind an instance to a static closure in %s on line %d
```

### 箭头函数

- 箭头函数和匿名函数都是 Closure 类实现的。
- 箭头函数（即便是嵌套的箭头函数也）可以自动地从父作用域捕获需要的变量。

``` php
$y = 1;

$fn1 = fn($x) => $x + $y;
// 等价写法
$fn2 = function ($x) use ($y) {
    return $x + $y;
};

var_export($fn1(3));
```

``` php
fn(array $x) => $x;
static fn(): int => $x;
fn($x = 42) => $x;
fn(&$x) => $x;
fn&($x) => $x;
fn($x, ...$rest) => $rest;
```

### 严格类型

参见[PHP手册：严格类型](https://www.php.net/manual/zh/functions.arguments.php#functions.arguments.type-declaration.strict)

默认情况下，如果能做到的话，PHP将会强迫错误类型的值转为函数期望的标量类型。 例如，一个函数的一个参数期望是string，但传入的是integer，最终函数得到的将会是一个string类型的值。

可以基于每一个文件开启严格模式。在严格模式中，只有一个与类型声明完全相符的变量才会被接受，否则将会抛出一个TypeError。 唯一的一个例外是可以将integer传给一个期望float的函数。

严格类型适用于在启用严格模式的文件内的函数调用，而不是在那个文件内声明的函数。 一个没有启用严格模式的文件内调用了一个在启用严格模式的文件中定义的函数，那么将会遵循调用者的偏好（弱类型），而这个值将会被转换。

``` php
declare(strict_types=1);

function sum(int $a, int $b) {
    return $a + $b;
}

var_dump(sum(1, 2));
var_dump(sum(1.5, 2.5));

// Output:
// int(3)

// Fatal error: Uncaught TypeError: Argument 1 passed to sum() must be of the type integer, float given, called in - on line 9 and defined in -:4
// Stack trace:
// #0 -(9): sum(1.5, 2.5)
// #1 {main}
//   thrown in - on line 4
```

## 面向对象编程

``` php
class SimpleClass
{
    public $var = 'a default value';
    public $dp

    public function __construct() {
        $dp = array{1 => 1, 2 => 2}
    }

    public function displayVar() {
        echo $this->var;
    }
}
```
