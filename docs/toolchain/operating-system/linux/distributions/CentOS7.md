# CentOS笔记

## 常用软件

1. 利用DeltaRPM减少下载体积

```sh
yum install deltarpm
```

## Software Collection

仓库由软件爱好者维护，在不修改系统软件的同时获得较新的软件。

- Software Collection[文档][]包含在各种Enterprise OS中启用仓库的指导。
- 需要安装特定软件时，可在[目录][]中搜索。

[文档]: https://www.softwarecollections.org/en/docs/
[目录]: https://www.softwarecollections.org/en/scls/

### 常用软件

1. devtoolset-* 包含gcc、g++等。

### 常用指令

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
