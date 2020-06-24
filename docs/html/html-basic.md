# HTML基本操作

## 视口

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```

## 使用层叠样式表CSS

详见[css.md](css/README.md)

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
