# HTML: Hyper Text Markup Language 笔记

## 视口

固定移动设备的缩放比例。

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```

<https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag>

## 标签（元素）

规范

```html
<p>This is a paragragh.</p>
```

HTML5允许没有结束标签的标签，这样的标签称为“空标签”或“自包含标签”。

常用标签

- 锚anchor `<a href="..."> </a>`
- 注释 `<!-- 注释 -->`
- 标题“块级元素” `<h1>` ... `<h6>`
- 段落 `<p>`
- 折行 `<br>`
- 水平线 `<hr>`
- 块级元素`<div>`，内联显示元素`<span>`

语义标签

- 文本格式化 b, big, em(emphasis), i, small, strong, sub, sup, ins, del
- 计算机 code, kbd(keyboard document), samp(sample), tt(teletype text), var, pre
- 引用标签 abbr, acronym, address, bdo(bi-direction override), blockquote, q(quote), cite, dfn(define)

语义化Div

- header
- nav
- main
- footer

### 属性

```html
<p style="font-family:arial; color:red; font-size:20px;">
    This is A paragraph.
</p>
```

- title
- href
- src
- style 用样式定义颜色，背景色，字体等，而不是用标签
- width  && height
- alt 替换文本
- background 背景图像
- align （弃用）对齐图像等 bottom middle top left right

## 使用层叠样式表CSS

详见[css.md](css.md)

## 使用JavaScript

```html
<script type="text/javascript">
    // Script goes here.
</script>
```

```html
<script type="text/javascript" src="..." charset="utf8"></script>
```

可以省略`type="text/javascript"`属性，因为JavaScript已成为默认浏览器脚本语言。

## 转义字符

- " `&quot;`
- & `&amp`
- Empty space `&nbsp`
- `&#数字`

## 超链接

target: _blank（新页面打开） _top（跳出框架）
name / id: label (href="#label")

发送邮件

```html
<a href="mailto:someone@microsoft.com?cc=someoneelse@microsoft.com&bcc=andsomeoneelse2@microsoft.com&subject=Summer%20Party&body=You%20are%20invited%20to%20a%20big%20summer%20party!">发送邮件！</a>
```

## 列表

- 列表 ol, ul, dl(description list)
- 列表项目 li

## 图像

站点图标

`<link rel="icon" href="favicon.ico" type="image/x-icon">`

## 音频和视频

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

text, checkbox, radio, hidden, password, submit, reset

```html
<form action="service.php">
<input type="text" name="email" id="email">
<input type="submit"> <input type="reset">
</form>
```

如果忽略action属性，表单提交到当前url。表单中的各项内容是根据name属性来区分的。

botton, textarea, select

```html
<select>
    <option>默认选项</option>
    <option value="IE">Internet Explorer</option>
</select>
```

- tabindex
- accesskey

---

## 参考链接

文档和规范

- [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [W3C语法验证器](https://validator.w3.org)
- [HTML5 标准](http://www.w3.org/TR/html)

资源

- [CSS禅意花园](http://csszengarden.com/)
