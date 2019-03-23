# Oracle 11g

- **[发行时间](https://en.wikipedia.org/wiki/Oracle_Database#Releases_and_versions)** 2007-2013
- [下载地址](https://www.oracle.com/technetwork/database/enterprise-edition/downloads/112010-win64soft-094461.html)
- 典型安装目录 `C:\\app\\username\\product\\11.2.0\\dbhome_1`

## OCI / OCCI Oracle C++ Call Interface

使用C++进行编程的接口。

在原始安装中包含了VC8和VC9编译的版本（`安装位置\\OCI`），在索引页面中包含了VC10编译的版本。

- [索引页面](https://www.oracle.com/technetwork/cn/database/features/oci/index-090820-zhs.html)
- [程序员指南](https://docs.oracle.com/cd/B28359_01/appdev.111/b28390/toc.htm)

## 局域网网络连接

使用Net Configuration Assistant重新配置网络就能让局域网络能够连接，原因不明。

目测是将`listener.ora`中的`localhost`换成了局域网络中设备的标志名`computer-name.lan`。
