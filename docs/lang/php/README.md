# PHP常识

- PHP（HyperText Preprocessor）：语法上与C语言相近，用于网页服务器的脚本语言。
- 通常需要与 Nginx 或 Apache 配合使用。

## 输出错误报告

``` php
error_reporting(E_ALL);
```

---

## 安装和配置

- 在Windows下安装PHP时，特别注意取消`extension_dir`部分的注释；否则将在尝试加载拓展时报错。
