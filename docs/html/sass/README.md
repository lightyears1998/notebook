# Sass预处理器

关于`scss`与`sass`代码格式（及同名的拓展名）：

1. 使用scss拓展名。
2. scss拓展名（代码格式）与sass肉眼可见的区别是，sass不具有分号和标志缩进的大括号。

## 命令行

```sh
sass <input-file> <output-file>
sass <input-dir>:<output-dir>
```

## 变量

```scss
$varible: value;
```

## 嵌套

```scss
div {
    h1 {
        // ...
    }
    p {
        // ...
    }
}
```

## SASS嵌入

```scss
// _base.scss
$var: val;

// main.scss
@use 'base';

tag {
    property: $var;
}
```

## 混合

```scss
@mixin transform($property) {
  -webkit-transform: $property;
  -ms-transform: $property;
  transform: $property;
}

.box { @include transform(rotate(30deg)); }
```

## 继承

```scss
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}

.message {
  @extend %message-shared;
}

.success {
  @extend %message-shared;
  border-color: green;
}

.error {
  @extend %message-shared;
  border-color: red;
}

.warning {
  @extend %message-shared;
  border-color: yellow;
}
```

## 运算

```scss
.container {
  width: 100%;
}

article[role="main"] {
  float: left;
  width: 600px / 960px * 100%;
}

aside[role="complementary"] {
  float: right;
  width: 300px / 960px * 100%;
}

```

---

<https://sass-lang.com/guide>
