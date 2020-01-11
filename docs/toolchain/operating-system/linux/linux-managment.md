# Linux系统管理

## 在系统/终端启动时运行脚本

- `~/.bash_profile`
- `/etc/profile`或`/etc/profile.d/*.sh`

## 自定义SSH欢迎文本

- tty `/etc/issue` `man issue` `man getty`
- Message of Today `etc/motd`

## 创建Swap文件

<https://linuxize.com/post/create-a-linux-swap-file/>

## 设置网络代理

```sh
export http_proxy=127.0.0.1:1080
export https_proxy=127.0.0.1:1080
```
