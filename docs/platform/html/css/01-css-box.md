# 盒模型

margin, boarder, padding

- margin
- boarder
- padding
- width, height

## `box-sizing`

- content-box width 和 height 只计算 content 的。
- border-box  width 和 height 算 content + border。

**外边框塌陷** 两个框彼此接触时，间距取两个相邻外边界的最大值而非两者之和。

## 相关属性

- margin, margin-top, margin-right, margin-bottom, margin-left
- padding, padding-top, padding-right, padding-bottom, padding-left

注意：

- 使用**顺时针注记法**时，多个值之间不需要空格。

## 浮动

- float: left | right 元素浮动到其容器的左侧|右侧
- clear: left | right | both 清除浮动
- overflow

## `position: relative`

使用`position: relative`并定义`left`, `right`, `top`, `bottom`等属性，
可以使元素move *away* from正常的文档流中应当在的位置。

```css
h2 {
    position: relative;
    top: 10px;
} /* 将h2从原本文档流中的盒模型的top位置移远10px。注意视觉上h2是向着bottom移动。 */
```

## `position: absolute` 绝对定位

相对于父元素的定位，left, top, right, bottom的含义同上。

## `positiom: fixed`

相对于浏览器窗口的绝对定位，left, top, right, bottom的含义同上。

## float属性

从正常的流中取出，并且向父容器的`left`或者`right`移动。

```html
<!-- 显示两栏布局 -->
<head>
  <style>
    #left {
      float: left;
      width: 50%;
    }
    #right {
      float: right;
      width: 40%;
    }
    aside, section {
      padding: 2px;
      background-color: #ccc;
    }
  </style>
</head>
<body>
  <header>
    <h1>Welcome!</h1>
  </header>
  <section id="left">
    <h2>Content</h2>
    <p>Good stuff</p>
  </section>
  <aside id="right">
    <h2>Sidebar</h2>
    <p>Links</p>
  </aside>
</body>

```

## z-index

指定元素堆叠顺序，值较大的在上层。

## 居中

水平居中 `margin: auto`。
