# HTML常用标签

- 锚anchor `<a href="..."> </a>`
- 注释 `<!-- 注释 -->`
- 标题“块级元素” `<h1>` ... `<h6>`
- 段落 `<p>`
- 折行 `<br>`
- 水平线 `<hr>`
- 块级元素`<div>`，内联显示元素`<span>`

语义标签：

- 文本格式化 b, big, em(emphasis), i, small, strong, sub, sup, ins, del
- 计算机 code, kbd(keyboard document), samp(sample), tt(teletype text), var, pre
- 引用标签 abbr, acronym, address, bdo(bi-direction override), blockquote, q(quote), cite, dfn(define)

语义化Div：

- header
- nav
- main
- footer
- video, article, section

常见属性：

- title
- href
- src
- style
- width && height
- alt 替换文本
- background 背景图像

## 列表

- 列表 `ol`(ordered list), `ul`(unordered list), `dl`(description list)
- 列表项目 `li`(list item)

## 图像

站点图标

`<link rel="icon" href="favicon.ico" type="image/x-icon">`

## 嵌入音频和视频

```html
<video controls="controls">
    <source src="...mp3" type="audio/mpeg">
    <source src="...ogg" type="audio/ogg">
<video>
```

```html
<audio controls="controls" poster="sparky.jpg">
    <source src="...m4v" type="audio/mp4">
    <source src="...ogv" type="audio/ogg">
<audio>
```

## 表单

```html
<form action="service.php">
    <input type="text" name="email" id="email">
    <input type="submit">
    <input type="reset">
</form>
```

如果忽略action属性，表单提交到当前url。表单中的各项内容是根据name属性来区分的。

### input

- type属性：text, checkbox, radio, hidden, password, submit, reset
- placeholder属性：显示文本替代符
- required属性

### button, textarea, select

```html
<button type="submit">Button Text</button>
```

```html
<select>
    <option>默认选项</option>
    <option value="IE">Internet Explorer</option>
</select>
```

### 选择按钮

使用`checked`属性来指定默认选中。

#### radio

可以使用label标签来包装radio。label标签的`for`属性常设为radio的`id`属性。单选按钮组的radio的`name`属性应相同。

```html
<label for="indoor"><input id="indoor" type="radio" name="indoor-outdoor"> Indoor</label>
<label for="outdoor"><input id="outdoor" type="radio" name="indoor-outdoor"> Outdoor</label><br>
```

#### checkbox

可以使用label标签来包装radio。label标签的`for`属性常设为checkbox的`id`属性。

```html
<label><input type="checkbox" name="personality"> Loving</label>
<label><input type="checkbox" name="personality"> Lazy</label>
<label><input type="checkbox" name="personality"> Energetic</label><br>
```
