# CSS笔记

CSS = Cascading Style Sheet.

## 在HTML中使用

- 外部样式 `<link rel="stylesheet" href="stylesheet.css">`
- 嵌入式样式 `<style></style>`
- 内联样式 `<tag style="pro1: val; pro2: val;" />`

## 基础语法

```css
/* 多行注释 */

选择器 {
    声明属性: 属性值;
}

```

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

注意：

- `val`值可以不使用引号包围，但推荐使用单引号。

## 层叠和继承

1. 层叠次序
    1. 重要性 `!important`规则

        ```css
        selector {
            props: val !important
        }
        ```

    2. 不同级别的源代码顺序（越靠后越优先）
        - 浏览器默认设置
        - 外部样式
        - 嵌入式样式
        - 内联样式
        - html属性

    3. 专用性 id优先于class
    4. 源代码次序 靠后的源代码覆盖前面。

        注意无论class中的顺序如何制定，效果始终是由style等源代码处声明样式的顺序决定。

2. 继承
    1. `inherit`（继承父元素）, `initial`（使用用户代理设定）, `unset`（自然状态继承）
    2. `all` 速写属性

## 颜色

- “透明色” `transparent`
- 颜色名称 `red`
- 十六进制颜色码 `#FF0000`
- 简写十六进制颜色码 `#F00`=`#FF0000`
- rgb `rgb(255, 0, 0)` `rgba()`
- hsl `hsl(0~365, 100%, 50%)` `hsla()`

## 度量单位

- px, mm
- em（继承父元素的字体大小设置）, rem（默认基础大小）

## 变量

```css
:root { /* 在root中定义的变量全局可用 */
    --my-color: orange;
}

tag {
    --my-color: red;  /* 可在局部覆盖全局值 */
    background: var(--my-color, black);  /* black是未定义时的默认值 */
}
```

## `@`规则

### 媒体查询

```css
@media (max-width: 350px) {
    :root {
        --penguin-size: 200px;
        --penguin-skin: black;
    }
}
```

---

## 参考

- [Mozilla CSS参考](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS禅意花园](http://csszengarden.com/)

## 颜色选择工具

1. [Colors on the Web](http://www.colorsontheweb.com/Color-Tools/Color-Wizard) 众多颜色工具。
2. [Paletton.com](http://paletton.com) 在色环上选择并且提供颜色使用示例。
3. [Adobe Color CC](https://color.adobe.com) 强大的色环工具，并且提供从图像中自动提取色彩的工具。
