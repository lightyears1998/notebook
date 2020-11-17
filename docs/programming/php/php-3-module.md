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

### 参数类型约束（参数类型声明）

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

- `$this` 是到主叫对象的引用。注意 PHP 中可以从类外或其他类的对象调用类的函数；
- 从实例调用方法使用 `$instance->method`；静态调用使用 `ClassName::method`。
- 类的属性和方法处于不同的“空间”，因此类的属性和方法可以重名。
- `ClassName::class` 返回类的完全限定名称字符串。

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

### `new`

``` php
$instance = new MyClass;
$instance = new MyClass();
$instance = new 'MyClass';
```

在类的内部还可以使用 `new self` 和 `new parent`，在类的 static 方法中可以使用 `new static` 获取类的新实例。

### 构造函数 `__construct`

- 在子类中定义了构造函数后，不会自动调用父类的构造函数。可以显式调用 `parent::__construct()`。
- 旧的构造函数是与类名同名的函数。

### 析构函数 `__destruct`

- 不会自动调用父类的析构函数，可以显式调用 `parent::__destruct()`；
- 析构函数即使在 `exit()` 终止运行时也会被调用，而在析构中调用 `exit()` 会终止其余关闭操作的运行。
- 试图在析构函数（在脚本终止时被调用）中抛出一个异常会导致致命错误。

### 继承 `extends`

- `class A extends B`
- 子类可以重载（overload）父类中定义的方法（final 除外），使用 `parent::`访问被覆盖的方法或属性。
- 覆盖函数时，参数必须保持一致。（构造函数除外。）

### 抽象 `abstract`

- 如果一个方法是抽象的，那么类也必须定义为抽象的。

### 接口 `interface`

- 可以在接口中定义抽象函数，以便在工厂模式中使用。

### `final`

- 如果父类中的方法被声明为 `final`，则子类无法覆盖该方法；
- 如果一个类被声明为 `final`，则不能被继承。

### 属性

- 属性使用 `public`、`protected` 或 `private` 声明。
- 属性可以在声明时初始化，但初始化值必须是常数。

### 类常量

- 使用 `const` 声明类常量。

### Trait

为传统的继承增加水平特性的组合。

- 从基类继承的成员会被 trait 插入的成员所覆盖。优先顺序是来自当前类的成员覆盖了 trait 的方法，而 trait 则覆盖了被继承的方法。
- 可以使用多个 trait 的组合，方法是使用逗号分割 trait 列表。
- 两个 trait 插入同名的方法时，需要使用 `insteadof` 解决冲突。
- 可使用 `as` 建立别名，或调整访问控制。
- trait 可以声明抽象方法，以对使用这个 trait 的类施加强制要求。
- trait 可以定义属性；类不能定义与 triat 同名的属性，但属性兼容（相同的访问控制以及默认初始值）时例外。

``` php
trait A {
    public function smallTalk() {
        echo 'a';
    }
    public function bigTalk() {
        echo 'A';
    }
}

trait B {
    public function smallTalk() {
        echo 'b';
    }
    public function bigTalk() {
        echo 'B';
    }
}

class Talker {
    use A, B {
        B::smallTalk insteadof A;
        A::bigTalk insteadof B;
    }
}

class Aliased_Talker {
    use A, B {
        B::smallTalk insteadof A;
        A::bigTalk insteadof B;
        B::bigTalk as talk;
    }
}
```

``` php
trait HelloWorld {
    public function sayHello() {
        echo 'Hello World!';
    }
}

// 修改 sayHello 的访问控制
class MyClass1 {
    use HelloWorld { sayHello as protected; }
}

// 给方法一个改变了访问控制的别名
// 原版 sayHello 的访问控制则没有发生变化
class MyClass2 {
    use HelloWorld { sayHello as private myPrivateHello; }
}
```

### 匿名类

匿名类被嵌入普通类后，不能访问外部类的 `private` 或 `protected` 成员。

### 重载（Overloading）或称“解释器钩子（Interpreter Hooks）”

详见[PHP 手册：重载](https://www.php.net/manual/zh/language.oop5.overloading.php)

PHP 的重载是指动态地创建类的属性和方法。当调用当前环境下未定义或不可见的类属性或方法时，重载方法会被调用。所有的重载方法都必须被声明为 public。

> PHP中的"重载"与其它绝大多数面向对象语言不同。传统的"重载"是用于提供多个同名的类方法，但各方法的参数类型和个数不同。

- 在给不可访问属性赋值时，__set() 会被调用。`public __set ( string $name , mixed $value ) : void`
- 读取不可访问属性的值时，__get() 会被调用。`public __get ( string $name ) : mixed`
- 当对不可访问属性调用 isset() 或 empty() 时，__isset() 会被调用。`public __isset ( string $name ) : bool`
- 当对不可访问属性调用 unset() 时，__unset() 会被调用。`public __unset ( string $name ) : void`

``` php
<?php
class PropertyTest {
     /**  被重载的数据保存在此  */
    private $data = array();


     /**  重载不能被用在已经定义的属性  */
    public $declared = 1;

     /**  只有从类外部访问这个属性时，重载才会发生 */
    private $hidden = 2;

    public function __set($name, $value)
    {
        echo "Setting '$name' to '$value'\n";
        $this->data[$name] = $value;
    }

    public function __get($name)
    {
        echo "Getting '$name'\n";
        if (array_key_exists($name, $this->data)) {
            return $this->data[$name];
        }

        $trace = debug_backtrace();
        trigger_error(
            'Undefined property via __get(): ' . $name .
            ' in ' . $trace[0]['file'] .
            ' on line ' . $trace[0]['line'],
            E_USER_NOTICE);
        return null;
    }

    /**  PHP 5.1.0之后版本 */
    public function __isset($name)
    {
        echo "Is '$name' set?\n";
        return isset($this->data[$name]);
    }

    /**  PHP 5.1.0之后版本 */
    public function __unset($name)
    {
        echo "Unsetting '$name'\n";
        unset($this->data[$name]);
    }

    /**  非魔术方法  */
    public function getHidden()
    {
        return $this->hidden;
    }
}


echo "<pre>\n";

$obj = new PropertyTest;

$obj->a = 1;
echo $obj->a . "\n\n";

var_dump(isset($obj->a));
unset($obj->a);
var_dump(isset($obj->a));
echo "\n";

echo $obj->declared . "\n\n";

echo "Let's experiment with the private property named 'hidden':\n";
echo "Privates are visible inside the class, so __get() not used...\n";
echo $obj->getHidden() . "\n";
echo "Privates not visible outside of class, so __get() is used...\n";
echo $obj->hidden . "\n";
?>

Output:
Setting 'a' to '1'
Getting 'a'
1

Is 'a' set?
bool(true)
Unsetting 'a'
Is 'a' set?
bool(false)

1

Let's experiment with the private property named 'hidden':
Privates are visible inside the class, so __get() not used...
2
Privates not visible outside of class, so __get() is used...
Getting 'hidden'


Notice:  Undefined property via __get(): hidden in <file> on line 70 in <file> on line 29
```

- 在对象中调用一个不可访问方法时，__call() 会被调用。`public __call ( string $name , array $arguments ) : mixed`
- 在静态上下文中调用一个不可访问方法时，__callStatic() 会被调用。`public static __callStatic ( string $name , array $arguments ) : mixed`

``` php

<?php
class MethodTest
{
    public function __call($name, $arguments)
    {
        // 注意: $name 的值区分大小写
        echo "Calling object method '$name' "
             . implode(', ', $arguments). "\n";
    }

    /**  PHP 5.3.0之后版本  */
    public static function __callStatic($name, $arguments)
    {
        // 注意: $name 的值区分大小写
        echo "Calling static method '$name' "
             . implode(', ', $arguments). "\n";
    }
}

$obj = new MethodTest;
$obj->runTest('in object context');

MethodTest::runTest('in static context');  // PHP 5.3.0之后版本
?>

Output:
Calling object method 'runTest' in object context
Calling static method 'runTest' in static context
```

### 遍历对象

- 默认情况下所有可见的属性都可通过 `foreach` 遍历。
- 可实现 `Iterator` 接口或 `IteratorAggregate` 接口以自行决定如何遍历。

### 魔术方法

- `__sleep()` 和 `__wakeup()`
- `__toString(): string`
- `__invoke([$...]): mixed` 当函数的方式调用一个对象时
- `__set_state(): object` 当以 `var_export()` 导出时
- `__debuginfo(): array` 当以 `var_dump()` 时

### 对象复制 `clone`

使用 `clone` 关键字来复制对象。PHP 对对象的所有属性进行一个浅拷贝。复制完成后，若有 `__clone` 方法定义，则新对象的 `__clone` 方法会被调用，以便修改属性的值。

### 对象比较

- `==` 如果两个对象的属性和属性值 都相等，而且两个对象是同一个类的实例，那么这两个对象变量相等。
- `===` 这两个对象变量指向某个类的同一个实例（即同一个对象）。

### 类的自动加载

- 使用 `spl_autoload_register()` 来自动加载脚本中所缺失的类。该函数组织一个 autoload 的队列。
- `__autoload()` 不建议使用，因为 `__autoload` 函数能只定义一次。

``` php
spl_autoload_register(function ($class_name) {
    require_once $class_name . '.php';
});

$obj  = new MyClass1();
$obj2 = new MyClass2();
```

### 后期静态绑定

难以理解的内容，需要学习 PHP 解释器源码，使用时必须参考[手册](https://www.php.net/manual/zh/language.oop5.late-static-bindings.php)。
