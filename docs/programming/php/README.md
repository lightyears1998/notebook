# PHP 常识

- PHP（HyperText Preprocessor）：语法上与C语言相近，用于网页服务器的脚本语言。
- 通常需要与 Nginx 或 Apache 配合使用。

## CLI

- `php -a` 命令行交互模式
- `php -r " echo PHP_VERSION; "` 直接运行代码

## 输出错误报告

``` php
error_reporting(E_ALL);
```

---

## 安装和配置

- 在Windows下安装PHP时，特别注意取消`extension_dir`部分的注释；否则将在尝试加载拓展时报错。

## 调试

PHP 的调试需要 `xdebug` 支持，在 Linux 发行版中通常不与本体打包在同一个模块中，需要[独立安装](https://xdebug.org/docs/install)。

``` sh
# 可通过查看版本信息检查 xdebug 安装情况。
php --version
```

(xdebug v2) 建议加入以下设置以便启用 step debugging 等调试功能。

``` conf
xdebug.mode = develop,debug,trace
xdebug.remote_enable = 1
xdebug.remote_autostart = 1
```

VS Code 通过 `felixfbecker.php-debug` 拓展提供调试支持。
