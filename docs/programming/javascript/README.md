# JavaScript常识

- 能解释清楚 JS 理论的 [The JavaScript language on JavaScript.info](https://javascript.info/js)

## 概述

- ECMAScript 是 JavaScript 的语言标准，JavaScript 是 ECMAScript 的一种实现。
- JavaScript 算是一种嵌入式语言，本身没有IO函数，需要宿主来提供。最典型的宿主是浏览器和服务器端的 Node 项目。
- JavaScript 不是纯粹的面向对象语言，也支持其他编程范式，例如函数式编程。
- JavaScript 的核心语法部分十分精简，只包含基本的语法构造和标准库，更多地依赖于宿主环境提供的 API。

## 基础语法

语句以分号结尾；表达式不需要以分号结尾。没有内容的语句是空语句。

## 编程风格

1. Javascript中区块起首的大括号紧跟在关键字后面，避免[难以察觉的错误](https://wangdoc.com/javascript/features/style.html#区块)。
2. 尽量使用严格相等运算符`===`，以避免[自动类型转换带来的不确定性](https://wangdoc.com/javascript/features/style.html#相等和严格相等)。
3. `switch... case`结构可以用面向对象结构替代。

    ```js
    function doActions(action) {
        var actions = {
            'one': function () {
                return 1;
            },
            'two': function () {
                return 2;
            },
            'run': function () {
                return 'run';
            }
        };

        if (typeof actions[action] !== 'function') {
            throw new Error('Invalid action.');
        }

        return actions[action]();
    }
    ```

4. 严格模式，在产生任何实际运行效果的语句前添加`'use strict'`字符串。

## 开发环境

### 控制台与 Console 对象

向控制台输出信息，自动在连续两个参数产生的输出间添加空格，并在每次输出的结尾添加换行符。

1. `console.log()`, `console.debug()`, `console.info()`
2. `console.warn()`
3. `console.error()`

支持格式字符串，如`%s`, `%d`或`%i`, `%f`, 对象的链接`%o`。

可以按自己的需要覆盖console的方法，如为console的输出添加时间字符串。

```js
['log', 'warn', 'error'].forEach(function (method) {
    console[method] = console[method].bind(
        console,
        new Date().toISOString()
    );
});
```

`console.table`可以将符合类型的数据转换为表格显示。

```js
console.table(
    {
        Alice: { name: 'Alice Kane', score: 32 },
        Bob: {name: 'Bob Kingdom', score: 44 }
    } // 或数组类型
);
```

- `console.dir()`用于对对象进行审察，格式比直接使用`console.log()`美观。
- `console.count('tag')`用于计数，输出它被调用了多少次。
- `console.time('tag')`和`console.timeEnd('tag')`用于计算操作花费的时间。
- `console.group()`, `console.groupEnd()`和`console.groupCollapsed()`用于对大量信息进行分组。
- `console.trace()`用于显示调用栈。
- `console.clear()`用于清空输出。

---

## 参考链接

- [ECMAScript文档](https://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf)
- [Mozilla JavaScript 参考](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [网道](https://wangdoc.com/javascript/)
