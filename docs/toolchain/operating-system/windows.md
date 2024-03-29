# Windows操作系统笔记

- 用户主目录的`AppData`下的`Local`包含各应用程序的临时文件（`Local\Programs`可存放可执行程序），`LocalLow`包含应用运行在保护模式下的临时数据（不常用），`Roaming`包含可漫游到其他机器数据，如应用程序配置等。

## 休眠

- `powercfg.exe /A` 报告系统可用的睡眠状态
- `powercfg.exe /hibernate off` 禁用休眠（和快速启动）

注：在电源菜单中关闭“休眠”功能的显示，并不能禁用休眠。曾有 Windows 更新会重新开启休眠。

## 输入法选项

- 在Windows微软拼音输入法中启用小鹤双拼
  1. 在注册表编辑器中定位到`\HKEY_CURRENT_USER\Software\Microsoft\InputMethod\Settings\CHS`项；
  2. 添加字符串项`UserDefinedDoublePinyinScheme0`，值`小鹤双拼*2*^*iuvdjhcwfg^xmlnpbksqszxkrltvyovt`；
  3. 在输入法设置中启用小鹤双拼。

## C++ Build Tools

- 最简单的做法是使用Build Tool for Visual Studio，即便不安装IDE也可以进行编译。
- 还可以直接使用Windows SDK。

## Hyper V选项

```cmd
REM 在具有管理员权限的命令提示符中
bcdedit /copy {current} /d "Windows 10 no Hyper-V"
bcdedit /set {上一个命令输出的GUID} hypervisorlaunchtype Off
bcdedit
```

## UWP选项

- 解除 UWP 本地环回限制 <https://stackoverflow.com/questions/33259763/uwp-enable-local-network-loopback> or [Loopback Manager](https://github.com/tiagonmas/Windows-Loopback-Exemption-Manager)

## 常量

```cmd
USERPROGRAMS="C:\Users\<username>\AppData\Local\Programs"
```

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

- [HxD](https://mh-nexus.de/en/hxd/) 文件二进制编辑工具
-
  - [WinDirStat](https://windirstat.net/) 磁盘空间管理工具。
  - DiskGenius 磁盘管理工具
  - FastCopy 文件快速复制

- [spacedeck](http://spacedesk.com/) 将Android手机屏幕作为Windows的拓展显示器。
- NSSM, *the Non-Sucking Service Manager* Windows服务注册工具
- [Rufus](https://rufus.ie/) USB启动盘制作工具
- Teleport Ultra 网页缓存工具
- PotPlayer 视频播放器

程序员环境：

- MSYS2

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

## 激活

- HEU_KMS_Activator <https://github.com/zbezj/HEU_KMS_Activator>
- 软件资源 <https://tb.rg-adguard.net/public.php>
