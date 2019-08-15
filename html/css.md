# Cascading Style Sheet笔记

## 在HTML中使用

- 外部样式 `<link rel="stylesheet" href="stylesheet.css">`
- 嵌入式样式 `<style></style>`
- 内联样式 `<tag style="pro1: val; pro2: val" />`

### 基础语法

```css
/* 多行注释 */

选择器 {
    声明属性: 属性值;
}

```

**@规则** 用于传递描述性的信息

### “层叠”次序

渲染方式优先级别

- 浏览器默认设置
- 外部样式
- 嵌入式样式
- 内联样式
- html属性

## 选择器

1. 简单选择器
    1. `tag` 元素名选择器
    2. `.class` 类选择器
    3. `#id` ID选择器
2. 属性选择器
    1. 存在和值（Present and Value）选择器
        - `[atrr]`
        - `[attr=val]`
        - `[attr~=val]`（属性包含val的元素，以空格为分隔符）
    2. 字串（Substring）属性选择器
        - `[attr|=val]` 选择以`val`或`val-`开头的元素
        - `[attr^=val]` 选择以`val`开头的元素
        - `[atrr$=val]` 选择以`val`结尾的元素
        - `[attr*=val]` 包含`val`的元素
3. 伪类和伪元素选择器
    1. `:status` 伪类选择器，如`:hover`等
    2. `::position` 伪元素选择器，如`::before`等
4. 组合器和多个选择器
    - `a, b` 选择A或B
    - `a b` A的子节点B
    - `a > b` A的直接子节点B
    - `a + b` A的相邻兄弟节点（B紧跟在A之后）
    - `a ~ b` 通用兄弟选择器（B为A之后兄弟节点的任意一个）

注意到`val`不需要引号。

## 值和单位

### 值

- 数值
- 百分比
- 颜色
- 坐标位置
- 函数

### 单位

- px
- em（继承父元素的字体大小设置）, rem（默认基础大小）

## 颜色

- 颜色名称 `red`
- 十六进制颜色码 `#FF0000`
- 简写十六进制颜色码 `#F00`
- rgb `rgb(255, 0, 0)` `rgba()`
- hsl `hsl(0~365, 100%, 50%)` `hsla()`

## 层叠和继承

1. 层叠次序
    1. 重要性 `!important`规则
    2. 专用性 id优先于class（使用个位、十位、百位和千位来衡量）
    3. 源代码次序 靠后的源代码覆盖前
2. 继承
    1. `inherit`（继承父元素）, `initial`（使用用户代理设定）, `unset`（自然状态继承）
    2. `all` 速写属性

```css
selector {
    props: val !important
}
```

## 图像

- 图像互换格式 GIF 256色 透明 动画 无损 交错
- 联合照片专家小组 JEPG 数百万色 无透明 无动画 有损 渐进式
- 可移植网络图形格式 PNG 数百外色 透明 无动画 无损 交错
- webp

## 中文字体

使用[Font.css](https://github.com/zenozeng/fonts.css)。

使用`woff`，字体子集化等技术来分发中文字体。

## 盒 border

- border-width
- border-style
- border-color

margin, boarder, padding

- margin
- boarder
- padding
- width, height

浮动

- float: left | right 元素浮动到容器的左侧|右侧
- clear: left | right | both 清除浮动
- overflow

**外边框塌陷** 两个框彼此接触时，间距取两个相邻外边界的最大值而非两者之和。

## 常用属性

字体

- font-size
- font-family

颜色

- color
- backgrond-color

图像

- background-image
- background-repeat
- background-position
- background-attachment
- background-clip 背景图像的绘制区域
- background-origin 背景图像的位置
- background-size

圆角和阴影

- border-radius
- box-shadow
- opacity 透明度

渐变

- background-image: linear-gradient(to bottom, #FFFFFF, #00FF00);

## Grid

### 创建布局

1. `grid-template-columns: 20% 20% 20% 20% 20%;`

    还可以使用百分比以外的数值来标定宽度，例如：`px`, `em`和Grid特有的单位`fr`（按比例分配格点时使用，每个`fr`为一份）

    使用fr作为单位时，fr的宽度将在最后计算，`grid-template-columns: 50px 1fr 1fr 1fr 50px;`。

2. `grid-template: <row> / <column>`是上述代码的简写

### 指定行与列

使用负数来标定行或列时，`-1`是指逆序第一条网格线。

1. `grid-column-start`, `grid-column-end`结合使用时，渲染结果是`[两者中较小值, 较大值)`（即夹在初始格线与停止格线之间的部分）
2. `span`可用于在给出了`start`或`end`时，指定格子拓展的长度
3. `grid-column: <start> / <end>;`是上述语法的简写

类似的还有`grid-row`的使用。

1. `grid-area: <row-start> / <column-start> / <row-end> / <column-end>;`是上述语法的简写

未指定`grid-column-start`等位置元素时，元素按源代码中出现的顺序占据一个格点，使用`order: <number>`来改变默认排序，类似于`z-index`。

### 辅助计算

1. `repeat(5, 20%)`展开为`20% 20% 20% 20% 20%`

这个参数顺序挺满足英语简单部分前置的风格的。

## Flex布局

```raw
+----------------------------> 主轴方向 flex-flow
|       justify-content 主轴上元素的留白策略
|
|
|       align-content 单行无效，
|                     多个伸缩行之间的留白策略
|
|
|  align-items
|  交叉轴上元素的留白策略
|
v
交叉轴方向 flex-wrap
```

## 参考链接

文档和规范

- [Mozilla CSS参考](https://developer.mozilla.org/en-US/docs/Web/CSS)

颜色选择工具

1. [Colors on the Web](http://www.colorsontheweb.com/Color-Tools/Color-Wizard) 众多颜色工具
2. [Paletton.com](http://paletton.com) 在色环上选择并且提供颜色使用示例
3. [Adobe Color CC](https://color.adobe.com) 强大的色环工具，并且提供从图像中自动提取色彩的工具
