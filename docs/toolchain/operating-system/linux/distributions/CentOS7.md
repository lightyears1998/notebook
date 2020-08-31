# CentOS笔记

- 最小安装之后，虚拟机内的网络功能可以通过 `nmtui` 进行配置。安装 `net-tools` 包以获得常用网络工具。

## 基本软件

```sh
yum install deltarpm # 利用DeltaRPM减少下载体积
```

## 包管理器YUM

> 除了包管理器YUM，还有值得注意的[Software Collection](#Software%20Collection)。

在`/etc/yum.repos.d`中管理源，基本的源有CentOS、EPEL和IUS源。
通常没有后缀的软件包是EPEL包，后缀为`u`的是IUS包。

自定义源统一定义在[`3rdparty.repo`](https://github.com/lightyears1998/code-sandbox/blob/master/toolchain/operating-system/linux/distributions/CentOS/3rdparty.repo)以便管理。

```sh
yum update
yum list [package-name] [installed | available | all]
yum search
yum install [package-name]
yum erase [package-name]

yum autoremove
```

## Software Collection

仓库由软件爱好者维护，在不修改系统软件的同时获得较新的软件。

- Software Collection[文档][]包含在各种Enterprise OS中启用仓库的指导。
- 需要安装特定软件时，可在[目录][]中搜索。

[文档]: https://www.softwarecollections.org/en/docs/
[目录]: https://www.softwarecollections.org/en/scls/

### 常用的Software Collection软件包

1. devtoolset-* 包含gcc、g++等。

### 常用的Software Collction指令

```sh
scl --list # 列出已安装的所有软件
scl enable
```

### 为所有shell启用通过Software Collections安装的软件

可在`profile.d`中创建脚本，并添加需要默认启用的软件。

```sh
#!/bin/sh
# etc/profile.d/enable-software-collections.sh
source scl_source enable devtoolset-8
```
