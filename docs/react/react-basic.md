# React基础知识

可以使用`create-react-app`快速新建使用React的单页面项目（SPA）。

```sh
npx create-react-app <app-name>
```

```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
```

## JSX

- 使用`{ }`插入JS表达式。
  - 表达式返回`null`时不插入。
  - 可以将JSX元素作为变量传递。
- 使用`htmlFor`来指明html的`for`属性；使用`className`来指明html的`class`属性。
