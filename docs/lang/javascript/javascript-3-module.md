# JavaScript模块

## 类与对象

对象是一种容器，封装了属性和方法。

JavaScript的对象基于原型链

### 构造函数

```js
var ChessBoard = function () {
  this.length = 8;
};
```

1. 构造函数内部使用了`this`关键字，表示所要生成的对象的实例
2. 调用构造函数必须使用`new`命令

### `new`命令

```js
var v = new ChessBoard(arg);
```

如果不使用`new`命令，构造函数将成为普通函数，不能生成实例对象。通常this引用全局对象，造成意想不到的结果。

#### 确保使用`new`命令

1. `'use strict'`
    严格模式中this不能引用全局对象，默认为`undefined`

    ```js
    function Foobar(foo, bar) {
      'use strict'
      this.foo = foo;
      this.bar = bar;
    }

    Foobar()  // TypeError: Cannot set property 'foo' of undefined
    ```

2. 构造函数内部判断是否使用`new`命令

    ```js
    function Foobar(foo, bar) {
      if (!this instanceof Foobar) {
        return new Foobar(foo, bar);
      }

      this.foo = foo;
      this.bar = bar;
    }
    ```

#### `new`命令的原理

1. 创建一个空对象，作为将要返回的实例
2. 将这个空对象的原型，指向构造函数的`prototype`属性
3. 将这个空对象赋给函数内部的this关键字
4. 执行构造函数内部的代码

若构造函数内部有return语句，且return后面指定了一个对象，则返回return语句指定的对象；否则返回this对象。

若对普通函数使用new命令，则返回一个空对象。

#### `new.target`

函数内部可以使用`new.target`属性。如果当前函数是`new`命令调用，`new.target`指向当前函数，否则为`undefined`。

### Object.create()

以现有对象为模板创建对象

### `this`

`this`总是返回一个对象。

`this`是属性或方法“当前”所在的对象（当前所在的运行环境），即只要函数被赋值给另一个对象（或其他运行环境的改变），`this`的指向就会改变。

必要时，可以使用中间变量固定`this`；必要时，应该绑定`this`。

应该避免，

1. 使用多层this
2. 在数组方法中使用this
3. 在回调函数中使用this

### `this`的绑定

- `Function.prototype.call(obj, arg1, arg2, ...)` 将函数内部的this指定到obj上，然后所指定的作用域中调用该函数。
- `Function.prototype.apply(obj, [arg1, arg2, ...])` 同call，但接受数组形式的参数
- `Function.prototype.bind(obj)` 将函数内部的`this`绑定到obj上，并返回一个新函数

#### 使用环境

1. 全局环境下`this`指代顶层对象`window`
2. 构造函数中`this`指代实例对象
3. 如果对象的方法中包含`this`，则`this`指向方法运行时所在的对象

注意JavaScript的方法是可以单独取出来使用的，如`foo.bar();`，此时`this`将指向全局环境。

如果`this`所在的对象不在第一层，则this只是指向当前一层的对象，不会继承上层对象。

### 继承

实例对象的`prototype`属性指向原型对象。

只要修改原型对象，变更就会体现在所有实例对象上。

原型对象的作用即定义所有实例对象所共享的属性和方法。

#### 继承链

所有对象的原型可以追溯到`Ojbect.prototype`，`Ojbect.prototype`的原型是`null`，原型链到此为止。

覆盖（Overwhelming），实例对象定义了与原型对象相同的方法。

#### `constructor`属性

可获知实例对象是由哪一个构造函数产生的。

#### `instanceof`

判断对象是否为某个构造函数的实例。

对于`null`和`undefined`，`instanceof`总是返回false。

### Object方法

#### `in` 运算符

检查对象是否具有某个属性

## ES6模块

From: <https://medium.com/@etherealm/named-export-vs-default-export-in-es6-affb483a0910>

Named export:

```js
// imports
// ex. importing a single named export
import { MyComponent } from "./MyComponent";
// ex. importing multiple named exports
import { MyComponent, MyComponent2 } from "./MyComponent";
// ex. giving a named import a different name by using "as":
import { MyComponent2 as MyNewComponent } from "./MyComponent";

// exports from ./MyComponent.js file
export const MyComponent = () => {}
export const MyComponent2 = () => {}

import * as MainComponents from "./MyComponent";
// use MainComponents.MyComponent and MainComponents.MyComponent2 here
```

Default export:

```js
// import
import MyDefaultComponent from "./MyDefaultExport";

// export
const MyComponent = () => {}export default MyComponent;
```
