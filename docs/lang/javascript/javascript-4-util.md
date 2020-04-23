# JavaScript工具

## 标准库

### Object

Object所有其他对象继承自`Object`对象，所有对象都是`Object`的实例。

#### `Object()`

`Object()`将任意值转换为对象，常用于保证某一个值一定是对象。

```js
var obj = Object();
// 等同于
var obj = Object(null);
var obj = Object(undefined);
obj instanceof Object;

// 如果参数是原始类型，则将其转换为对应包装器的类型
var obj = Object('string');
obj instanceof Object;
obj instanceof String;

// 如果方法的参数为对象，则不进行转换
// 由此可写一个判断参数是否为对象的函数
function isObject(value) {
    return value === Object(value);
}

isObject([]);    // true
isObject(true);  // false

```

`Object()`可以作为构造函数使用

```js
var obj = new Object();
// 等价于
var obj = {};

// 如果构造函数的参数是一个对象，则直接返回该对象
var o1 = { a: 1 };
var o2 = new Object(o1);
o1 === o2;  // true

var obj = new Object(123);
obj instanceof Number;  // true

```

#### Object的静态方法

指部署在Object对象自身的方法。

1. 遍历对象自身的属性（而不是继承的属性），可枚举属性`Object.keys()`，还包括不可枚举属性的`Object.getOwnPropertyNames()`
2. 对象属性模型相关方法
    1. `Object.getOwnPropertyDescriptor()` 获取某个属性的描述对象
    2. `Object.defineProperty()` 通过描述对象定义属性
    3. `Object.defineProperties()` 通过描述对象定义多个属性
3. 控制对象状态的方法
    1. `Object.preventExtensions()` 防止对象被拓展
    2. `Object.isExtensible()` 判断对象是否可拓展
    3. `Object.seal()` 禁止对象配置
    4. `Object.isSealed()` 判断对象是否可配置
    5. `Object.freeze()` 冻结对象
    6. `Object.isFrozen()` 判断对象是否被冻结
4. 原型链相关方法
   1. `Object.create()` 可以指定原型对象和属性，返回新的对象
   2. `Object.getPrototypeOf()` 获取对象的prototype对象

#### Object的实例方法

部署在`Object.prototype`对象的方法。

1. `Object.prototype.valueOf()`返回当前对象对应的值。
2. `Object.prototype.toString()`, `Object.prototype.toLocaleString()`返回当前对象对应的字符串形式。
    通过Object.prototype.toString()可以判断一个对象的类型
3. `Object.prototype.hasOwnProperty()`判断某个属性是否为当前对象自身的属性，还是继承自原型对象的属性。
4. `Object.prototype.isPrototypeOf()`判断当前对象是否为另一个对象的原型对象
5. `Object.prototype.propertyIsEnumerable()`某个属性是否可枚举

### 属性描述对象 Atrributes Object

JavaScript内部用于描述属性的对象，用于控制对象属性的行为等。

属性描述对象的例子

```js
{
  value: 123,
  writable: false,      // 属性是否可改变
  enumerable: true,     // 若不可枚举则在一些操作中会被跳过，如 (for ... in)和Object.keys()
  configurable: false,  // 是否可删除该属性，是否可改变描述属性对象的值
  get: undefined,       // getter
  set: undefined
}
```

```js
var obj = { p: 'a' };

Object.getOwnPropertyDescriptor(obj, 'p');
```

#### `Object.defineProperty(object, propertyName, attributesObject)`

为object定义属性，并返回对该object的引用。

```js
var o = Object.defineProperty({}, 'p', {
    value: 123,
    writable: true,
    enumerable: true,
    configurable: true
});

```

### Array对象

`Array`既是原生对象，又是构造函数。

### Array的构造函数

不同参数时行为不同。

1. 无参数返回空数组。
2. 单一数值参数返回指定长度的空数组；负值参数报错。
3. 单一非数值参数，将该参数作为返回新数组的成员。
4. 多参数，将参数作为返回数组的成员。

#### `isArray()`

用于判定指定参数是否为数组，弥补`typeof`的不足。

```js
var arr = [1, 2, 3];

typeof arr;  // object
Array.isArray();
```

#### Array的实例方法

1. `valueOf()`, `toString()` `valueOf()`返回数组本身，`toString()`返回数组的字符串形式。
2. `push()`, `pop()` 添加或弹出数组中的最后一个元素；对空数组使用`pop()`将不报错而返回`undefined`
3. `shift()`, `unshift()` 在数组的第一个位置删除或添加元素，此方法返回新的长度。
4. `join(separator = ',')` 将数组的所有元素以指定分隔符连接为字符串。
5. `concat()` 将参数数组的成员合并到原数组中；**原数组不变**，返回合并后的新数组。
6. `reverse()` 颠倒原数组。
7. `slice(start, end)` 提取目标数组的一部分，返回新数组，**原数组不变**。可以接受负数的参数。若没有参数，实际上时创建元素组的拷贝；因此可以借助此方法将类似数组的对象转换为真正的数组。
8. `splice(start, howmany, addElement1, addElement2, ...)` **改变原素组** 拼接；删除指定位置的元素，并将后续参数加入原数组。
9. `sort()` 将数组元素进行排序。默认按字典序进行排序（注意数值将被转换为字符串再进行排序）。可以传入函数作为参数，按自定义方法进行排序。

    `sort`自定义排序与C++ STL的`sort()`返回值的意义相反，注意区分。

    ```js
    [1, 2, 3].sort(function (cur, nxt) {
        return nxt > cur;  // 若返回的数值大于0，则表示nxt的位置应排在cur前；否则均排在cur后面。
    });  // [3, 2, 1]

    ```

10. `map()` 将数组的每一个成员依次传入参数函数，并将执行的结果合并成一个数组返回。`forEach()`类似于`map()`但是不获取返回值，仅仅用于操纵数据。这两种方法都会跳过数组中的空位，但不会跳过`undefined`和`null`。

    ```js
    var out = [];

    [1, 2, 3].forEach(function (elem, index, arr) {
        this.push(2 * elem + index);
    }, out);
    ```

11. `filter()` 对每个元素执行filter中的函数，将函数返回结果为`true`的元素组成新的数组，返回新的数组。

    ```js
    [1, 2, 3].forEach(function (elem, index, arr) {
        return true;
    }, /* 可绑定函数中的this变量 */)

    ```

12. `some()`, `every()` 对数组中的每个元素执行函数，若某些/每个元素的执行结果为`true`，则返回`true`。
13. `reduce()`, `reduceRight()` 对数组中的每个元素执行函数，`reduceRight()`从右往左执行，函数接受四个参数

    ```js
    var arr = [1, 2, 3, 4, 5];

    arr.reduce(function (prev /*积累变量，默认值为arr[0] */, cur /* 当前变量，默认为arr[1] */, index, arr) {
        return prev + cur;  // 返回值作为下一次执行函数时的prev值
    });  // 数组求和
    ```

    `reduce()`函数的第二个参数可对积累变量赋初始值，注意此时`cur`变量为数组中的第一个元素。这里可以避免由于空数组无法取得初始值时出错。当没有初始值时，`reduce`从索引1开始执行callback，否则，从索引0开始执行callback。
14. `indexOf()`, `lastIndexOf()` 给出给定元素在数组中出现的位置，如果没有出现则返回`-1`。第二个参数表示开始搜索的位置。
    注意此方法不能用于搜索`NaN`的位置，因为`NaN`是唯一自身不等于自身的值。

### 包装对象

数值、字符串和布尔值有对应的包装对象`Number`, `String`和`Boolean`。

自动转换生成的包装对象是只读的；自动转换调用完毕后包装对象会自动销毁。

可以在包装对象的原型上定义新的方法。

### Number对象

具有一些有用的静态属性，如`Number.MAX_SAFE_INTEGER`, `Number.POSITIVE_INFINITY`

有用的实例方法：

1. `toString(不大于16的进制数)`
2. `toFixed(指定小数位数)`
3. `toExponential(小数位数)`
4. `toPrecision(指定位数的有效数字)`

### String对象

静态方法

1. `fromCharCode(unicode1, unicode2, ...)` 返回对应码点组成的字符串。码点大于0xFFFF的字符需要连续使用两次或以上此方法
2. `charCodeAt()` 上述方法的逆方法
3. `trim()` 去除字符串两端的空白字符，返回新字符串，**不改变原字符串**。
4. `toLowerCase()`, `toUpperCase()`
5. `match()`, `search()`, `replace()` 正则方法
6. `split()` 使用指定分隔符分割字符串，返回包含分割字符串的属猪；如果未指定分隔符，则返回数组的唯一成员为原字符串；如果指定分隔符为空字符串，则返回数组成员为原字符串的每一个字符。

具有类似数组的方法。

注意到`substring()`或`substr()`与`slice()`不同，会自动将参数中的负数转换为0，违反直觉。因此建议使用`slice()`

### Math对象

不是构造函数，所有属性和方法都必须在Math对象上调用。

### Date对象

1. 直接调用 无论有没有参数，`Date()`都返回代表当前时间的字符串
2. 构造函数用法
    1. 可以被`Date.parse()`解析的字符串都可以作为字符串参数
    2. 单一数值为毫秒数
    3. `new Date(year, month, day, hour, minute, second, microsecond0~999)` 参数可以使用0和负数；注意月份从0开始计算，但天数从1开始计算

注意日期的直接运算，相加为字符串的拼接，相减为毫秒数的相差（参考自动类型转换）

静态方法

1. `Date.now()` 当前时间的毫秒数。
2. `Date.parse()` 通常是`YYYY-MM-DDTHH:mm:ss.sssZ`格式，最后的Z表示时区；其他格式也能被解析。解析成功返回毫秒数，解析失败返回`NaN`
3. `Date.UTC()` 将参数当成UTC时间进行解释。其他与Date构造函数相同。

实例方法

1. `toString`, `toISOString`(等价于`toJSON`)
2. `toDateString`, `toTimeString`
3. `getDate()`等
4. `setDate()`等

### JSON对象

对值的类型和格式有严格的规定

> 1. 复合类型的值只能是数组或对象，不能是函数、正则表达式对象、日期对象。
>
> 2. 原始类型的值只有四种：字符串、数值（必须以十进制表示）、布尔值和`null`（不能使用`NaN`, `Infinity`, `-Infinity`和`undefined`）。
>
> 3. 字符串必须使用双引号表示，不能使用单引号。
>
> 4. 对象的键名必须放在双引号里面。
>
> 5. 数组或对象最后一个成员的后面，不能加逗号。

1. `JSON.stringnify()` 可接受第二个参数（数组或函数）定制输出内容，第三个参数（字符串）定制缩进字符。
2. `JSON.parse()`

### RegExp对象

仿照Perl 5体系的正则表达式。

```js
var reg1 = /reg/igm                   // 字面值
var reg2 = new RegExp('reg', 'igm');  // 对象形式

```

#### RegExp的实例属性

1. 只读
    - 与修饰符相关的`RegExp.prototype.ignoreCase`, `global`, `multiline`。
    - 返回正则表达式的字符串形式 `RegExp.prototype.source`。
2. 可写 下一次搜索时开始的位置，`RegExp.prototype.lastIndex`，只在进行连续搜索时有意义。

#### RegExp的实例方法

1. `test` 当前模式是否能匹配参数字符串。
2. `exec` 返回匹配字符串。

## Chapter 7+ 文档对象模型DOM

### 节点Node

DOM的最小组成单位，包括7种：

1. Document 文档根节点
2. DocumentType doctype标签
3. Element html标签
4. Attribute 元素属性
5. Text 标签之间或标签包含的文本
6. Comment 注释
7. DocumentFragment 文档片段

以上7种节点继承自Node对象

### 节点树

`document`节点代表整个文档

节点之间的关系：父节点、子节点、同级节点。

### Node接口

### NodeList接口和HTMLCollection接口

### ParentNode接口和ChildNode接口

### 属性的操作

- `getAttribute()`, `getAttributeNames()`
- `setAttribute()`
- `hasAttribute()`, `hasAttributes()`
- `removeAttribute()`

### Canvas

#### 绘图上下文

```js
ctx = canvas.getContext('2d');
```

#### 绘制图形

绘制矩形

- `fillRect(x, y, width, height);`
- `strokeRect(x, y, width, height);`
- `clearRect(x, y, width, height);`

绘制路径

- `beginPath()`
- `moveTo(x, y)`
- `lineTo(x, y)`
- `closePath()`
- `storke()`, `fill()`

### URLSearchParams

构造、解析和处理URL的查询字符串。
