# PHP基础

PHP通过PHP解释器解释执行，通常是结合Apache或Nginx在Linux或Windows操作系统上使用。

- `<?php expression; ?>`
- 直接输出表达式的值 `<?= expression ?>`
- `echo expression;`

## 注释

```php
# Life is like a box of chocolate.

// Life is like a box of chocolate.

/**
 * Life is like a box of chocolate.
**/
```

## 数据类型

数据类型在运行时决定。

- 四种标量类型：布尔型（boolean），整型（integer），浮点型（double，float或real），字符串型（string）
- 两种符合类型：数组（array），对象（object）
- 两种特殊类型：资源（resource），无类型（NULL）

工具函数

- `gettype()` 返回boolean, integer, double, string等字符串
- `(boolean)`, `(bool)`, `(integer)`, `(int)`, `(float)`, `(double)`, `(string)`
- `floatval()`, `intval()`, `floatval()`, `strval()` 注意`int()`等是未定义的方法

变量类型转换

- 自动转换 `(type)$var` 作用是临时的
- 强制转换 `settype($var, 'int')` 作用是持久的

### 布尔型

值取`TRUE`, `FALSE`，赋值时可不区分大小写

echo输出时，对于TRUE的变量输出1，对于FALSE变量输出空字符串。

当值被转换成boolean类型时，被认为是FALSE的值的类型

- `FALSE`
- 0, 0.0, 空字符串, 字符串“0”
- 不包括任何元素的数组array
- NULL（包括尚未赋值的变量）
- 从空标记生成的SimpleXML对象

任何其他值都被认为是TRUE（包括任何资源）

### 整型

```php
$num = 1234;
$num = 0234;  // 八进制
$num = 0x34;  // 十六进制
```

高精度拓展：BC Math，GMP

### 浮点型

### 字符串

- 单引号字符串 `'string'`
- 双引号字符串 `"string"`

用双引号定义的字符串，其中的变量会被解析，并且转义特殊字符。

```php
$hel = 'hel';
echo "$hel lo"  // 可解析
echo "$hello"   // 不可解析，提示未定义变量
```

heredoc

```php
<<<EOT
多行字符串
EOT

// EOT无引号包围，如同使用双引号包围
// 注意最后的EOT标记必须单独成一行，即没有缩进，其后也没有其他字符
```

heredoc会对其中变量解析并且转义特殊字符

```php
$a = 'test'
$str = <<<EOD
a = $a\n
EOD;
echo $str;  // 输出test并附加换行符
```

nowdoc

```php
<<<'EOT'
多行字符串
EOT
```

nowdoc不解析变量也不转义

```php
$a = 'test'
$str = <<<'EOD'
a = $a\n
EOD;
echo $str;  // 输出test并附加换行符
```

- Hereodc: Here is a document and parse is needed.
- Nowdoc: The document is now parsed.

字符串的连接使用`.`操作符，而不是`+`操作符。

### 数组

数组：有序映射

- 定义数组 `array{"a"=>"apple", "b"=>"banana"};` 短定义语法 `['a'=>1, 'b'=>2]`
- 访问数组元素 `array[key]`, `array{key}`
- 打印数组 `var_dump()`, `print_r()`

php支持多维数组

#### 数字索引数组

自动设置键名

```php
$food = array("饼干", "巧克力", "蛋糕");
$food[] = "瓜子";  // 设置键名为3
```

此外还有关联索引数组

#### 数组指针

数组中有内部指针，指向当前的元素。foreach不会移动数组内部指针。

`current()`, `each()`以数字索引数组和关联索引数组形式返回键名和键值，并移动, `end()`, `next()`, `prev()`

#### 工具函数

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

### 对象

`new`

### 资源

`$handle = fopen($filename, $filemode);`

### 无类型

未被赋值或被赋值为NULL，或被`unset()`的变量

- `is_null()`
- `unset()`
