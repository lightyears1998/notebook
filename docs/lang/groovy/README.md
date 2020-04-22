# Groovy常识

Apache基金会下Java平台的脚本语言。

## 语法特色

文档：[与Java的不同](https://groovy-lang.org/differences.html)

- 分号可以省略
- 括号在不产生歧义时可以省略，如`print 1 + 10`
- Groovy没有Java中的`Primitive type`，所有原始类型都使用对应包装类
- 使用`def var`或`Typename var`来定义变量；类型明确的前提下可以省略`def`或`Typename`
- 自动导入以下包和类型
    1. java.lang, java.util, java.io, java.net
    2. groovy.lang, groovy.util
    3. java.math.BigInteger, Java.math.BigDecimal

---

## 安装Groovy

在Windows平台上访问[官网下载](https://groovy.apache.org/download.html)页面。
