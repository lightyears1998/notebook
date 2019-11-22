# Windows操作系统笔记

## MSYS2

一般选择安装`mingw-w64-x86_64-toolchain`，而不是`gcc`，从而可以将`C:\msys64\mingw64\bin`加入PATH。
从而避免将`C:\msys64\usr\bin`加入PATH，以免导入不需要的UNIX工具。

```sh
pacman -Sy
pacman -Syu # 更新所有包
pacman -Ss gcc # 搜索
pacman -S <package-name>
```

## 輸入法繁簡切換

默認：Ctrl + Shift + F

## 软件包管理

[Chocolatey](https://chocolatey.org/)

```ps1
# 以管理员身份运行
choco install <package-name>
choco upgrade <package-name>
```

图形界面：`choco install chocolateygui`

## 磁盘空间管理

- [WinDirStat](https://windirstat.net/)

## 拓展显示器

- [spacedeck](http://spacedesk.com/) 将Android手机屏幕作为Windows的拓展显示器。

## 连接到使用Windows的远程计算机

`Ctrl + ALT + BREAK`可在之间全屏/窗口化之间切换。

- 远程桌面连接
  - [更改远程桌面连接监听的端口号](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/change-listening-port) 特别注意在“Windows高级安全防火墙”中放开更改后的端口。
- 远程命令 [Powershell Remoting](https://docs.microsoft.com/zh-cn/powershell/scripting/learn/remoting/running-remote-commands?view=powershell-6)
- 大规模文件传输 使用远程桌面挂载磁盘或使用FileZilla Server等建立FTP服务器。
