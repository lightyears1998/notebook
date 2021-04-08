# Terminal

## tmux

`tmux` 可以使命令可以独立于 SSH 的 Shell 环境运行，以免程序在连接中断时自动停止。

``` shell
# 初次运行
$ tmux
$ pipenv run python cclangkit/app.py

# 在 tmux 中按下 Ctrl+B, $ 组合键可重命名 Session。
# [Ctrl+B, $] cclangkit [Enter]

# 脱离会话
# [Ctrl+B, d]

# 打开上次会话
$ tmux list-sessions
$ tmux attach -t cclangkit
```
