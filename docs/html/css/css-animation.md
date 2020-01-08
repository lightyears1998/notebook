# CSS动画

- 使用`url(...)`导入网址中的图片。
- 使用`transform: scale(2)`将元素的大小变为默认大小的两倍。
- 线性渐变 `background: linear-gradient(gradient_direction, color 1, color 2, color 3, ...);`

## 动画效果

```css
p:hover {
    transform: scale(2)
}
```

```html
<!-- 使用skewX沿着水平方向歪斜。 -->
<style>
  div {
    width: 70%;
    height: 100px;
    margin:  50px auto;
  }
  #top {
    background-color: red;
  }
  #bottom {
    background-color: blue;
    transform: skewX(24deg);
  }
</style>

<div id="top"></div>
<div id="bottom"></div>
```

```html
<!-- 心形 -->
<style>
  .heart {
    position: absolute;
    margin: auto;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    background-color: pink;
    height: 50px;
    width: 50px;
    transform: rotate(-45deg);
  }
  .heart::after {
    background-color: pink;
    content: "";
    border-radius: 50%;
    position: absolute;
    width: 50px;
    height: 50px;
    top: 0px;
    left: 25px;
  }
  .heart::before {
    content: "";
    background-color: pink;
    border-radius: 50%;
    position: absolute;
    width: 50px;
    height: 50px;
    top: -25px;
    left: 0px;
  }
</style>
<div class="heart"></div>
```
