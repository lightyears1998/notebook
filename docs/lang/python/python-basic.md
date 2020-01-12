# Python基础

## 命名规范

<http://google.github.io/styleguide/pyguide.html#3164-guidelines-derived-from-guidos-recommendations>

## 注释

```python
# 一行中“#”之后的内容为注释。

"""
Docstring可用作模块或函数的注释。
"""

def shout(word):
  """
  Print a word with an
  exclamation mark following it.
  """
  print(word + "!")

shout("spam")
```

## 数据类型

### 六类基本数据类型

| 类型 | 备注 |
| --- | --- |
| 数值类型 `int`, `float`, `bool`, `complex` | |
| 字符串 `String` | 由成对出现的单引号或双引号创建。 |
| 元组`Tuple` | 由小括号`()`创建。 |
| 列表`List` | 由中括号`[]`创建。 |
| 字典`Dictionary` | 由花括号`{key: value}`创建，单独的花括号为空字典。 |
| 集合`Set` | 使用花括号`{value}`或者`set()`创建，必须用`set()`创建空集合，因为花括号默认用于创建`Dictionary`。 |

其中：

- 不可变类型 *Immutable*： `Number`, `String`, `Tuple`
- 可变类型 *Mutable*：`List`, `Dictionary`, `Set`

使用工具方法`type(variable)`查看variable的类型。

### `None` 无类型

未定义返回类型的函数返回`None`。

```python
# `None`可被转换成布尔类型值的`False`。
if None:
  # won't execute
```

### 数值类型

包括`int`, `float`, `bool`和`complex`四类数值类型。

可进行四则运算：

- 浮点除法 `/` 整除 `//`
- 取模、浮点取模 `%`
- 乘方 `**`

数值运算工具：

- `min()`, `max()`
- `abs()`
- `sum(列表)` 对list对象元素求和。

#### 数值类型的类型转换

从其他类型转换到数值类型：

- `True`, `False`在参与数字运算时分别转化为1和0。
- `int()` 转换为整数类型。
- `float()` 转换为浮点数类型。

将数值类型转换为字符串：

- `str()`
- `bin()` 将整数转换为二进制字符串。

```python
>>> bin(7)
'0b111'
```

### `String` 字符串

用成对`''`或`""`来声明，单引号与双引号无区别。字符串内部以Unicode表示。

参与数值运算：

- 不能与数字直接相加。
- 与整数的乘法，如`str * 3`会复制字符串。
- str之间相加合并字符串，不能相减。

工具函数（由于String是不可变对象，以下工具函数都是异地的）：

- `分隔符.join([字符串列表])` 形如PHP中的`implode()`，利用分割符合并字符串。
- `str.startswith()`, `str.endswith()` 返回真与假。
- `str.replace('what', 'with')` 将字符串中的所有`what`替换为`with`。
- `str.upper()`, `str.lower()` 字符串全文大小写转换。
- `str.split('separator')` 分割字符串为列表。

#### 使用`format()`格式化字符串

```py
nums = [4, 5, 6]
msg = "Numbers: {0}, {1}, {2}".format(nums[0], nums[1], nums[2])

msg = "({x}, {y})".format(x=5, y=2)
```

### `bytes`

```py
'ABC'   # string
b'ABC'  # bytes

>>> bytes('我歌唱每一条河', 'gbk')
b'\xce\xd2\xb8\xe8\xb3\xaa\xc3\xbf\xd2\xbb\xcc\xf5\xba\xd3'
```

构造函数：

- 字面值 `b'ABC'`
- `bytes('字符串', '编码名称')`

工具函数：

- `str.encode([encoding='gbk'])` 将str编码为bytes。
- `bytes.decode([encoding='ascii'])` 将bytes解码为str。

### `Tuple` 元组

- 元组与list行为类似，但它是immutable对象。使用小括号而不是方括号。
- 也可以不使用小括号，直接使用逗号分隔元素即可。

```py
# list
list = ["one", "two"]

# dictionary
dictionary = {1:"one", 2:"two"}

# tuple
tuple = ("one", "two")
tuple = "one", "two"
```

### `List` 列表

List使用方括号`[]`定义，下标从0开始。

```py
['1', '2', '3', ]  # List中只有3个元素
```

参与四则运算：

- list之间可以相加，但不能相减。
- list与数值间的乘法：`[1, 2, 3]*2`返回`[1, 2, 3, 1, 2, 3]`。列表与小于等于0的数相乘返回空列表。

方法：

- `append()`
- `insert()` 原位置元素后移
- `index()` 返回值的第一个索引位置，不存在时抛出`ValueError`

工具函数：

- `in` 操作符判断元素是否在List内。
- `len(list)` 返回List的长度。

### `Slicing` 切片方法

适用于List、Tuple及字符串。

- `[bgn:end:step]` 以步长step包含元素`[bgn, end)`，三个参数都不是必要的。
- 注意bgn可以大于end（所以上面那个区间的写法是错的😅），生成的方向总是从bgn到end，且不包含end
- 如果索引index为负数，它是指从后往前数第index个字符；`[2:-2]`生成`[2, 倒数第二个字符)`
- 若步长为负数，那么List会反向生成。`[::-1]`可反转数组。

#### Comprehensions 列表解析器

从数学的集合语法（set-builder notation）中脱胎的列表解析器

```py
cubes = [i**3 for i in range(5)]                     # [0, 1, 8, 27, 64]
evens = [i**2 for i in range(10) if i**2 % 2 == 0 ]  # [0, 4, 16, 36, 64]
```

滥用列表解析器可能产生MemoryError，可使用generator缓解。

### Set 集合

- 使用`set()`接受一个列表作为参数构建集合。
- 使用`add()` 添加元素。
- 集合间运算：合并`|`, 同时存在`&`, 不同时存在`^`, 差（第一个集合中包含而第二个集合中不包含）`-`。

### Dictionary 字典

```py
ages = {"Dave": 24, "Mary":42, "John":58}

print("Mary" in ages)      # True
print("Will" not in ages)  # True

ages.get("Dave")
ages.get("Hurry")          # 返回None
ages.get("Hurry", 34)      # 返回34
```

只有不变的（immutable）对象才能作为Dictionary的键，否则抛出KeyError。

```py
d: dict = {}

# 添加键值
d[k1] = v1
d.update({k2: v2})

# d == { k1: v1, k2: v2 }
```
