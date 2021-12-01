# Python工具

## `with`

```py
with open(filename) as f:
    text = f.read()
```

## `range()`

- `range(n)` 生成`[0, n)`的列表
- `range(i, j)` 生成`[i, j)`的列表
- `range(i, j, k)` 生成`[i, j)`的等差列表，公差为k

## 谓词 `all()`, `any()`

```py
nums = [55, 44, 33, 22, 11]

if all([i > 5 for i in nums]):
    print("All larger than 5")

if any([i % 2 == 0 for i in nums]):
    print("At least one is even")
```

## 遍历`enumerate()` 按键值对的方式遍历列表，返回元组

```py
for v in enumerate(nums):
    print(v)
```

## `itertools`

1. `count(value)` 从value开始向无穷计数
2. `cycle(iterable)` 开始iterable的无穷循环
3. `repeat()` 无限或有限次的重复
4. `chain(a, b, c)` 将 a, b, c 连接成一个列表 `[...a, ...b, ...c]`

```py
from itertools import count;

for i in count(3):
  print(i);
  if i > 10:
    break
```

1. `takewhile(pred, iterable)` 当谓词为真时继续循环
2. `chain()` 合并多个iterable
3. `accumulate()` 返回累计值

```py
from itertools import accumulate, takewhile

nums = list(accumulate(range(8)))
print(nums)  # [0, 1, 3, 6, 10, 15, 21, 28]
print(list(takewhile(lambda x: x<= 6, nums)))  # [0, 1, 3, 6]
```

1. `product()`
2. `permutation()`

```py
from itertools import product, permutations

letters = ("A", "B")
print(list(product(letters, range(2))))  # [('A', 0), ('A', 1), ('B', 0), ('B', 1)]
print(list(permutations(letters)))       # [('A', 'B'), ('B', 'A')]
```

## `random`

``` py
random.shuffle(listVar)
```

## 文件操作

### `open()` and `close()`

```python
# write mode
open("filename.txt", "w")

# read mode
open("filename.txt", "r")
open("filename.txt")

# binary write mode
open("filename.txt", "wb")

file.close()
```

#### 保证`close()`方法最终被调用

使用异常处理机制：

```python
try:
    file = open("in.txt")
finally:
    file.close()
```

使用with... as...机制：

```python
with open("in.txt") as file:
    printf(f.readlines())
```

### read()

```python
file = open("filename.txt", "r")
print(file.read(16)) # 按字节数量读取
print(file.read())   # 读取剩余文本
print(file.read())   # 输出空串
file.close()
```

```python
file = open("filename.txt", "r")
print(file.readlines(16)) # 返回list，按行分割，元素中包含换行符
```

### write()

`file.write(content)`

不附加换行符，返回写入文件的字符数量。

## 函数式编程

### `map(func, arg)`

使用iterable对象作为第二个参数，返回对每个参数进行func后的iterable。

### `filter(pred, arg)`

返回满足谓词的iterable对象。

## 正则表达式

```py
import re
pattern = r'regular_expression'
```

基本工具

1. `re.match(pattern, string)` 从字符串的开始尝试匹配模式，成功时返回`match`对象
2. `re.serach(pattern, string)` 扫描整个字符串，并返回第一个成功的匹配
3. `re.findall(pattern, string)` 返回所有匹配的子串

match示例

```py
import re

pattern = r"pam"

match = re.search(pattern, "eggspamsausage")
if match:
    print(match.group())
    print(match.start())
    print(match.end())
    print(match.span())

"""
>>>
pam
4
7
(4, 7)
>>>
"""
```

搜索和替换 `re.sub(pattern, repl, string, max=0)`

```py
import re

str = "My name is David. Hi David."
pattern = r"David"
newstr = re.sub(pattern, "Amy", str)
print(newstr)
```

### 正则元字符

1. `.` 除换行符外的任意字符
2. `^`, `$` 匹配行的开头和行的结尾
3. `[aeiou]`, `[a-z]`, `[0-9]` 匹配字符组中的一个；使用`[^A-Z]`来取反（排除大写字母）
4. `*` 0个或更多前述字符
5. `+` 1个或更多前述字符
6. `?` 0个或1个前述字符 `pattern = r'ice(-)?cream'`
7. `{x, y}` [x, y]个前述字符
8. `|` 或
9. `\数字n` 匹配前一形式的n次后续重复 如`r"(.+)\1"`将匹配形如"word word", "abc abc"的字符串
10. `\d`, `\s`, `\w` 数字，空白字符或word characters；`\D`, `\S`, `\W`前述功能的取反
11. `\b` 匹配`\w`与`\W`之间的空字符串（non-word characters与word characters之间的空字符串）如`\bcat\b`会匹配“The cat sat!”和“We s>cat<\tered?”但不会匹配“We scattered.”
12. `\A`与`\Z`分别输入的开头和结尾（与`^`和`$`区别）

### Group

`group(), group(0)`返回整个匹配，`group(n)`返回第n个匹配的组

可以通过`(?P<name>...)`的形式声明命名的组，并通过`group('name')`来访问

可以通过`(?...)`的形式声明non-capture组，non-catpure组不能通过group函数来访问

搜索邮件地址

```py
import re

pattern = r"([\w\.-]+)@([\w\.-]+)(\.[\w\.]+)"
str = "Please contact info@sololearn.com for assistance"

match = re.search(pattern, str)
if match:
   print(match.group())
```
