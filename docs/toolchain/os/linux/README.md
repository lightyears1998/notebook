# Linux操作系统笔记

## 终端Terminal

终端前的符号表示用户的权限等级：

- `$` normal user
- `#` Root user；`#`比`$`更接近0。

## 指令Commamnd

`command [-options] parameter1 parameter2...`

- 命令区分大小写。
- 可以使用反斜杠转义[Enter]，使命令跨行生效。
- `Ctrl + D` End of Input

实用命令：

- `cal [[month] year]`
- `date`
- `bc`

### 后台运行指令

- `Ctrl + Z`
- `(cmd &)`
- `bg [%jobnumber]`
- `fg [%jobnumber]`
- `nohup`

## 帮助系统

### Manual

- `man -f command` `whatis command` 列出command的手册
- `man -k keyword` `man -K keyword-in-text` `apropos command` 根据关键字列出command的手册
- `man [1-9] command`
- 使用`man man`查看9类数字说明符对应的含义
- `/string` `?string` 向下、向上查询字符串
- `n, N` 下一个 /上一个查询目标

### Info

- `info info`
- `h` 帮助系统
- `N P` 前后导航
- `U` 向上

## 启停控制

- `sync`将数据写入磁盘。
- `reboot`
- `halt`
- `poweroff`

### 运行级别Run-level

使用`init [number]` 切换运行级别。

1. LEVEL0 关机
2. LEVEL3 命令行模式 tty1 ~ tty6
3. LEVEL5 含有图形界面模式 tty7
4. LEVEL6 重启

### 图形管理员 Window Manager

- 重启X Windows `Ctrl + Alt + Backspace`
- 切换Terminal `Ctrl + Alt + [F1~F7]`

## 系统管理

### 自定义终端欢迎界面

- tty `/etc/issue` `man issue` `man getty`
- Message of Today `etc/motd`

### 创建Swap文件

<https://linuxize.com/post/create-a-linux-swap-file/>

### 系统/终端启动时自动运行脚本

- `~/.bash_profile`
- `/etc/profile`或`/etc/profile.d/*.sh`

## 文件编辑

`vi/vim`, `nano`

## 设置网络代理

```sh
export http_proxy=127.0.0.1:1080
export https_proxy=127.0.0.1:1080
```
