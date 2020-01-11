# Linux基本命令行

## 启停控制

- `sync` 将数据写入磁盘。
- `reboot`
- `halt`
- `poweroff`

### 运行级别Run-level

使用`init [number]` 切换运行级别。

1. LEVEL0 关机
2. LEVEL3 命令行模式 tty1 ~ tty6
3. LEVEL5 含有图形界面模式 tty7
4. LEVEL6 重启

## 图形界面：Window Manager

- 重启X Windows `Ctrl + Alt + Backspace`
- 切换Terminal `Ctrl + Alt + [F1~F7]`

## 进程调度

- `Ctrl + Z` 暂停前台任务
- `(commands &)` 在后台运行
- `jobs`
- `bg [%jobnumber]`
- `fg [%jobnumber]`
- `nohup`

---

## 帮助系统

### Manual

- `man -f command` `whatis command` 列出command的手册
- `man -k keyword` `man -K keyword-in-text` `apropos command` 根据关键字列出command的手册
- `man [1-9] command`
- 使用`man man`查看9类数字说明符对应的含义
- `/string` `?string` 向下、向上查询字符串
- `n, N` 下一个 /上一个查询目标

### Info

- `info <something>`。如：`info info`。
- 按下`h` 帮助系统，使用`N P`前后导航，`U` 向上导航。
