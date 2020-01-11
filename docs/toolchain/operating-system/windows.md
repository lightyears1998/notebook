# Windows操作系统笔记

## 快捷键

- `Win`: `+Space`, `+ArrowKey`, `+NumberRow`, `+Ctrl+ArrowKey`
- 微软拼音输入法
  - `Ctrl + Shift + F` 繁简
  - `Ctrl + Shift + B` 表情，即FF的Bookmarks
  - `Shift`, `Ctrl + Space` 中英切换
  - `Shift + Space` 全角半角
  - `Ctrl + .` 中英标点

## 软件包管理Chocolatey

使用PowerShell的包管理器；可安装图形界面：`choco install chocolateygui`（作用不大）。

```ps1
# 一些操作以需要管理员身份运行Powershell。
choco list --local-only
choco list <software-name>
choco install <software-name>
choco upgrade <software-name>
```

## 常用软件

1. [HxD](https://mh-nexus.de/en/hxd/) 文件二进制编辑工具
2. [WinDirStat](https://windirstat.net/) 磁盘空间管理工具
3. [spacedeck](http://spacedesk.com/) 将Android手机屏幕作为Windows的拓展显示器。

程序员环境：

1. MSYS2

    一般选择安装`mingw-w64-x86_64-toolchain`，而不是`gcc`，从而可以将`C:\msys64\mingw64\bin`加入PATH。
    从而避免将`C:\msys64\usr\bin`加入PATH，以免导入不需要的UNIX工具。

    ```sh
    pacman -Sy
    pacman -Syu # 更新所有包
    pacman -Ss gcc # 搜索
    pacman -S <package-name>
    ```

## 连接到使用Windows的远程计算机

- 远程桌面连接
  - [更改远程桌面连接监听的端口号](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/change-listening-port) 特别注意在“Windows高级安全防火墙”中放开更改后的端口。
  - `Ctrl + ALT + BREAK`可在远程桌面连接的全屏/窗口化之间切换。
- 远程命令 [Powershell Remoting](https://docs.microsoft.com/zh-cn/powershell/scripting/learn/remoting/running-remote-commands?view=powershell-6)
- 若需要进行大规模文件传输，可使用远程桌面挂载磁盘或使用FileZilla Server等建立FTP服务器。
