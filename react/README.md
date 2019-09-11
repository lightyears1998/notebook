# React.js

```js
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
```

## JSX

- 使用`{ }`插入JS表达式。
  - 表达式返回`null`时不插入。
  - 可以将JSX元素作为变量传递。
- 使用`htmlFor`来指明html的`for`属性。

## React Component

- 自定义的组件名以大写开头。
- 有且只有一个最外层元素。
- 组件可以相互嵌套。

### 事件监听

<https://reactjs.org/docs/events.html#supported-events>

- `on*`事件监听未经过特殊处理只能用于普通HTML标签。
- 要在事件中获取实例时，需要bind。`onClick={this.handleClickOnText.bind(this)}`

## State

使用`this.state`和`this.setState()`来管理状态。

```js
class LikeButton extends Component {
  constructor() {
    super();
    this.state = {
      isLiked: false
    };
  }

  handleOnClick() {
    this.setState({
      isLiked: !this.state.isLiked
    });
  }

  render() {
    return (
      <div onClick={this.handleOnClick.bind(this)}>
        {this.state.isLiked ? "Like" : "DisLike"}
      </div>
    );
  }
}
```

- `this.setState()`接收对象或函数。
- 使用`this.setState()`时，只需传入要修改的部分。
- `setState()`并不会马上修改值，而是将修改放入更新队列中。这样，无法使用修改后的值来做新的运算。
- 如果后一个操作需要前面`this.setState()`更新的值，可以使用接收函数作为参数的`setState()`，在函数中返回对象；注意此时`this.setState()`仍然只更新一次。

    ```js
    this.setState((prevState) => {
      return {
        count: prevState.count + 1
      };
    });
    ```

- 存在`setState`合并机制，不必担心性能问题。

## Props 拓展属性

- 使用JSX组件时，所有放置在参数中的属性会被传入当成`props`的键值对。

    ```js
    class LikeButton extends Component {
    render() {
        const textA = this.props.textA || "Text A";
        const textB = this.props.textB || "Text B";
        return (
        <div>
            <p>{textA}</p>
            <p>{textB}</p>
        </div>
        );
    }
    }

    ReactDOM.render(<LikeButton textA="Hello, haapy world."/>, document.getElementById("root"));
    ```

- 可以使用`defaultProps`来指定初始值。

    ```js
    class LikeButton extends Component {
        static defaultProps = {
            textA: "Text A",
            textB: "Text B"
        }

        render() {
            const textA = this.props.textA;
            const textB = this.props.textB;
            return (
                <div>
                    <p>{textA}</p>
                    <p>{textB}</p>
                </div>
            );
        }
    }
    ```

- `props`不可变，只能重新渲染。

## 函数式组件

React鼓励使用`props`而不是`state`，因为过多的状态管理会带来性能问题。

函数式组件是只能接收`props`和返回`render`方法的函数。

```js
const MakeSound = (props) => {
    const sound = props.sound || "Wha...";
    return (
        <p>{sound}</p>
    )
}
```

## 渲染数组元素

存放JSX的数组会被一个一个罗列并渲染。

```js
const users = [
  { name: "Jackson", age: 22 },
  { name: "Tomas", age: 24 },
  { name: "Jelly", age: 25 }
];

class UserList extends Component {
  render() {
    return (
      <div> {
        users.map((user) => {
          return (
            <div key={user.name}>
              <p>姓名：{user.name}</p>
              <p>年龄：{user.age}</p>
            </div>
          );
        })
      }
      </div>
    );
  }
}
```

为了使用Virtual-DOM的优化机制，每个列表项应该有一个全局唯一的`key`HTML属性。

## 处理用户输入

- **受控组件** 所有的状态都由state控制。

## 信息传递

- 由上层组件来管理信息。
- 借助下层组件的`props`属性来组织重新渲染。

不推荐的写法：（其实影响也不大。）

```js
this.state.comments.push(comment);
this.setState({
  comments: this.state.comments
});
```

推荐的写法：

```js
const comments = this.state.comments.slice();
comments.push(comment);
this.setState({
  comments: comments
});
```

---

## 使用`create-react-app`快速新建单页面项目

```sh
npx create-react-app <app-name>
```
