# Python模块

## 导入模块 Import Module

```python
import random
from math import pi
from math import sqrt as rt
```

## 函数Function

```python
def fun(arg1, arg2):
    # 函数体
```

参数类型限定

```python
def fun(arg: int) -> None:  # 函数返回类型
    # 函数体
```

默认参数

```py
def fun(arg="default"):
    # 函数体
```

可变数量的参数

```py
def function(named_arg, *args):
    print(named_arg)
    print(args)  # args是一个tuple
```

关键字参数Key word arguments（未提前定义的具名参数）

```py
def my_func(x, y=7, *args, **kwargs):
   print(kwargs)  # kwargs是一个字典

my_func(2, 3, 4, 5, 6, a=7, b=8)

"""
{'a': 7, 'b': 8}
"""
```

### Generator生成器

属于iteralbe，但不能随机存取

使用`yield`关键字从生成器函数中返回值

```py
def countdown():
  i = 5;
  while i > 0:
    yield i
    i -= 1

for v in countdown():
  print(v)
```

### Decorator 装饰器

不修改原始函数而拓展其功能的方法

```py
def decor(func):
  def wrap():
    print('=================')
    func()
    print('=================')
  return wrap
```

使用`@`注记可以使函数包含在decorator中

```py
@decor
def print_text():
  print("Hello world!")
```

## Lambda表达式

```py
# named function
def polynomial(x):
    return x**2 + 5*x + 4
print(polynomial(-4))

# lambda
print((lambda x: x**2 + 5*x + 4) (-4))
```

为Lambda表达式分配标识符 `double = lambda x: x * 2`

## 类

```py
class Cat:
  eyes = 'blue'

  __init__(self, color, legs):
    self.color = color
    self.legs  = legs
```

- `dir(obj)` 列举对象的属性和方法

### 构造器`__init__`

使用`self`作为第一个参数

### 静态方法与非静态方法

非静态方法的一个参数总是`self`，没有`self`作为参数的方法是静态方法

```py
Obj().method()  # 非静态方法
Obj.smethod()   # 静态方法
```

与工厂方法统一，静态方法可以使用`@staticmethod`修饰符

### 类方法（工厂方法）

类方法使用`@classmethod`修饰器，并接受`cls`作为第一个参数，返回类的一个实例

```py
class Square:
  def __init__(self, width, length):
    self.width = width
    self.length = length

  @classmethod
  def new_square(cls, side_length):
    return cls(side_length, side_length)
```

### 类继承

```py
class Animal:
  def __init__(self, name, color):
    self.name = name
    self.color = color

class Cat(Animal):
  def purr(self):
    print("Purr...")

class Dog(Animal):
  def bark(self):
    print("Woof!")
```

### `super`

使用`super`关键字调用同名的基类方法

### 魔术方法

方法名由两个下划线包围的方法称为魔术方法，如`__init__`和`__add__`

### 操作符重载

使用魔术方法来重载操作符

- __sub__ for -
- __mul__ for *
- __truediv__ for /
- __floordiv__ for //
- __mod__ for %
- __pow__ for **
- __and__ for &
- __xor__ for ^
- __or__ for |

重载比较

- __lt__ for <
- __le__ for <=
- __eq__ for ==
- __ne__ for !=
- __gt__ for >
- __ge__ for >=

含有特殊功能的重载

- __len__ for len()
- __getitem__ for indexing
- __setitem__ for assigning to indexed values
- __delitem__ for deleting indexed values
- __iter__ for iteration over objects (e.g., in for loops)
- __contains__ for in

### 封装

The Python philosophy is slightly different. It is often stated as **"we are all consenting adults here"**, meaning that you shouldn't put arbitrary restrictions on accessing parts of a class. Hence there are no ways of enforcing a method or attribute be strictly private.

以单下划线开头的类成员不会被和数据不会被`from module_name import *`自动导入

**名称隐藏**：以双下划线开头的类成员在外部引用时需要使用不同的名称，形如`_classname__method`的形式

```py
class Spam:
  __egg = 7
  def print_egg(self):
    print(self.__egg)

s = Spam()
s.print_egg()            # 7
print(s._Spam__egg)      # 7
print(s.__egg)           # AttributeError: 'Spam' object has no attribute '__egg'
```

### 属性

以字段的形式访问方法，从而使特定的字段只读或能通过方法自动生成。

支持Setter语法

```py
class Pizza:
    def __init__(self, toppings):
        self.toppings = toppings
        self._pineapple_allowed = False

    @property
    def pineapple_allowed(self):
        return self._pineapple_allowed

    @pineapple_allowed.setter
    def pineapple_allowed(self, value):
        if value:
            password = input("Enter the password: ")
            if password == "Sw0rdf1sh!":
                self._pineapple_allowed = value
            else:
                raise ValueError("Alert! Intruder!")

pizza = Pizza(["cheese", "tomato"])
print(pizza.pineapple_allowed)
pizza.pineapple_allowed = True
print(pizza.pineapple_allowed)
```

## 包装

```python
SoloLearn/
   LICENSE.txt
   README.txt
   setup.py
   sololearn/
      __init__.py
      sololearn.py
      sololearn2.py
```

还有py2exe这样的神奇的存在。
