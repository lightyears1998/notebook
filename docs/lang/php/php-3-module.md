# PHP模块

## 函数

在函数中可以通过`global`关键字获取全局变量，使用`static`关键字定义静态变量。

```php
function foo($arg1, $arg2, $arg3, ...)
{
    return $val;
}
```

函数具有全局作用域，可以在一个函数内定义而在这个函数外调用。

```php
function foo(&$var){
    // 通过引用传递参数
}
```

缺省参数只能位于函数参数表末端

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

`call_user_func($fun)` 运行回调函数

### 可变参数列表

```php
function foo(...$vars) {}
```

### 返回值类型声明

```php
function foo() : int {}
```

### 可变函数

```php
$functions = ['fun1', 'fun2', 'fun3'];
foreach($functions as $fun)
{
    $fun();
}
```

### 匿名函数

```php
$myfunction = function() {
    // body
};
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
