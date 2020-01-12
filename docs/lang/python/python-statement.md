# Python语句

## 变量与“常量”的声明语句

- 变量不需要声明类型。“变量就是变量，没有所谓类型”。变量“类型”是指变量所指向的内存中的对象的类型。
- 没有显式声明“常量”的方式。
- 通过赋值来声明变量，支持多变量赋值语法：
  
  ```python
  a, b, c = 2, 3, "5"
  ```

- 删除变量 `del variable_name`。

## 三元运算符Ternay Operator

```py
b = 1 if a >= 5 else 42
```

## 分支语句`if`

```python
if exp:
    # Something

if exp:
    # Something
else:
    # Something

if exp:
    # Something
elif exp2:
    # Something
else:
    # Something
```

## 循环控制语句`while`

```python
i = 0
while i <= 5:
    i = i + 1
```

`else`与配对时，如果循环不是以`break`方式退出，`else`语句块将被执行。

### foreach语句`for`

Python中没有C语言风格的`for`，注意到Python中的`for`实际上为`foreach`

```python
for word in words
    # Something

for i in range(5)
    # Something
```

## 异常处理

```python
try:
    # Something
except:
    raise # 重新抛出异常
except(Error, Error):

finally:
    # 即使产生未捕获的异常时也会执行

raise NameError("Invilid Name!")

assert exp # 断言失败即抛出异常
assert exp, "额外说明"
```

如果`else`与`try`块配对，仅当没有异常时会执行`else`里的语句。
