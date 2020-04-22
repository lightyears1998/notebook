# JavaScript语句

## 表达式

### 变量声明

对值的具名引用。没有赋值的变量的值是`undefined`。

使用`var`来声明变量；不使用`var`的声明可被执行。

```js
var a = 1 + 3;
```

- 变量具有动态类型。
- **变量提升** 所有使用`var`声明变量的语句都会被提升到代码的头部，并先执行。

### 在区块中的变量

对于`var`声明的变量来说，区块（Block）不构成单独的作用域（Scope）。

```js
{
  var a = 1;
}
a;  // 1
```

## 运算

### 加法运算

#### 加法运算符

1. 数值之间的相加是平凡的
2. 数值与布尔值的相加，布尔值先转换为数值（true转换为1）
3. 存在字符串的相加，数值转换为字符串，字符串合并

对于加法以外的运算符，操作数一律转换为数值再进行计算。

#### 对象的相加

1. 先将对象转换为原始类型的值，规则如下：
    1. 调用对象的`valueOf()` 一般对象的`valueOf()`返回自身
    2. 调用对象的`toString()` 默认返回`"[object Object]"`，可重写此方法
2. 相加

### 取余运算

运算结果的**符号**由**第一个**操作数决定。

可用于浮点数。

### 数值运算符

一元运算符`+`, `-`。可以将任何值转换为数值（与`Number()`作用相同）

### 指数运算符

`a ** b`

### 比较运算

#### 非相等运算符：字符串的比较

字符串的比较按Unicode码表进行。

#### 非相等运算符：非字符串的比较

1. 原始类型值转换为数值进行比较
2. 对象先调用`valueOf()`，若返回的结果仍是对象，则调用`toString()`方法

注意下面特殊的比较：

```js
[2] > [1] // true
// 等同于 [2].valueOf().toString() > [1].valueOf().toString()
// 即 '2' > '1'

[2] > [11] // true
// 等同于 [2].valueOf().toString() > [11].valueOf().toString()
// 即 '2' > '11'

{ x: 2 } >= { x: 1 } // true
// 等同于 { x: 2 }.valueOf().toString() >= { x: 1 }.valueOf().toString()
// 即 '[object Object]' >= '[object Object]'
```

#### 严格相等运算符

1. 类型不同则返回`false`
2. 同一类型的原始类型，比较值是否相等
3. 同一类型的复合类型（函数、对象、数组），比较是否指向同一个地址
4. `undefine`和`null`与自身严格相等；`NaN`与自身不相等`!=`，也严格不相等`!===`

#### 相等运算符

1. 类型相同时，与严格相等的判断方式一致
2. 类型不同时进行类型转换
    1. 原始类型的值转换成数值再进行比较
    2. 对象与原始类型的比较，对象先转换为原始类型的值
    3. `null`, `undefined`与其他类型的值比较时，结果均为`false`；相互比较时结果为`true`。

注意违反直觉的比较

```js
0 == ''             // true
0 == '0'            // true

2 == true           // false
2 == false          // false

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true

```

### void运算符

执行一个表达式，且不返回任何值（返回`undefined`）。

### 逗号运算符

对多个表达式求值，并返回后一个表达式的值。

### 运算符结合性

注意到指数运算符是右结合的。

## 分支语句和循环语句

- `if`, `switch`, `while`, `do... while`, `for`结构与C++保持一致。
- 可以像在Java语言中那样结合标签使用`break`和`continue`。

注意：

- `switch`表达式的匹配采用严格相等运算符`===`。

## 异步语句

见[javacript-async.md](javascript-async.md)

## 异常处理机制

`Error`实例对象具有错误消息`message`，通常还会具有错误名称`name`和调用栈`stack`信息。

原生JavaScript存在6个`Error`类的派生对象。

1. `SyntaxError`
2. `ReferenceError`
3. `RangeError`
4. `TypeError`
5. `URIError`
6. 不再使用的`EvalError`

可以自定义错误

```js
new Error('错误信息');

function UserError(message) {
    this.message = message || '默认信息';
    this.name = 'UserError';
}

UserError.prototype = new Error();
UserError.constructor.prototype = UserError;

new UserError('自定义错误信息');

```

使用`throw`抛出错误，使用`try ... catch()`捕获错误。

```js
try {
    // ...
}
catch (e) {
    if (e instanceof EvalError) {
        // ...
    }
    else if (e instanceof TypeError) {
        // ...
    }

    // 如果catch块中存在return或throw，将延迟到finally块后执行
}
finally {
    // 不管是否出错都在最后运行的语句
}
```
