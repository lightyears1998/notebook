# HTML基本操作

HTML = Hyper Text Markup Language.

## 结构

```html
<!DOCTYPE html>
<html>
<head></head>
<body></body>
</html>
```

## 视口

固定设备（多为移动设备）的缩放比例。

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```

参考：[MDN视口](https://developer.mozilla.org/zh-CN/docs/Mobile/Viewport_meta_tag)

## 标签（元素）

规范

```html
<p>This is a paragragh.</p>
```

HTML5允许没有结束标签的标签，这样的标签称为“空标签”或“自包含标签”。

### 属性

```html
<p style="font-family:arial; color:red; font-size:20px;">
    This is A paragraph.
</p>
```

## 使用层叠样式表CSS

详见[css.md](css)

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

结合Anchor标签使用`href`属性。

- `target`属性
  - 新页面打开`_blank`
  - 跳出框架`_top`
- 哑链接`href="#"`
- 页面内链接 `id="label"` `href="#label"`

### 发送邮件

```html
<a href="mailto:someone@microsoft.com?cc=someoneelse@microsoft.com&bcc=andsomeoneelse2@microsoft.com&subject=Summer%20Party&body=You%20are%20invited%20to%20a%20big%20summer%20party!">发送邮件！</a>
```

---

- [Mozilla Developer Network](https://developer.mozilla.org/en-US/docs/Web/HTML)
- [W3C语法验证器](https://validator.w3.org)
- [HTML5 标准](http://www.w3.org/TR/html)
