# Oracle 11g

- **[发行时间](https://en.wikipedia.org/wiki/Oracle_Database#Releases_and_versions)** 2007-2013
- **获取途径**
  - Express版本 <https://www.oracle.com/technetwork/cn/database/database-technologies/express-edition/overview/index.html>
  - Enterprise版本 <https://www.oracle.com/technetwork/database/enterprise-edition/downloads/112010-win64soft-094461.html>
  - 这些链接可能在不久后失效

## OCI / OCCI Oracle C++ Call Interface

使用C++进行编程的接口。

在原始安装中包含了VC8和VC9编译的版本（`安装位置\\OCI`），在索引页面中包含了VC10编译的版本。

- [索引页面](https://www.oracle.com/technetwork/cn/database/features/oci/index-090820-zhs.html)
- [程序员指南](https://docs.oracle.com/cd/B28359_01/appdev.111/b28390/toc.htm)

---

## 安装

### 在Windows上安装

- 默认应用程序端口 `8080`
- 默认TNS监听端口 `1521`

- 典型安装目录 `C:\\app\\username\\product\\11.2.0\\dbhome_1`

### 在Linux上安装

- 典型安装目录 `/u01/app/oracle/product/11.2.0/xe`

可参照[官方文档](https://docs.oracle.com/cd/E17781_01/install.112/e18802/toc.htm)进行安装。

> 虽然Oracle 11g Express，以现在的Windows风格的审美来看，并不美观，但运行在Cent OS上还是十分搭配的。这难道是成熟的商业软件的力量？
> 2019.03.29

SQLPlus

```sh
cd /u01/app/oracle/product/11.2.0/xe/bin
. ./oracle.sh  # 如有必要，设置Oracle环境变量
sqlplus
```

### 版本与兼容性问题

Instant Client的版本一般是向下兼容的，所以不需要为了连接Oracle 11g而使用版本11.2的Instant Client，使用现代的版本以配合现代的编译环境。

如果现在现代环境中使用旧版本的Instant Client，比如在VS2017中使用Instant Client 11.2，则需要注意：在调试时可能出现`MSVCR100.dll`缺失等由于VS1017无法安装v100平台工具集而无法正确解决的问题。（可以通过Dirty hack，在生成目录中放入`MSVCR100.dll`以使得程序不报错。）

## Windows上的局域网网络连接

使用Net Configuration Assistant重新配置网络就能让局域网络能够连接，原因不明。

目测是将`listener.ora`中的`localhost`换成了局域网络中设备的标志名`computer-name.lan`。

## 故障解决

在Linux上进行操作前需要配置环境变量。

```sh
source /u01/app/oracle/product/11.2.0/xe/bin/oracle_env.sh
```

### Linux ORA-27101

原因不明，症状如下：

```txt
ERROR:
ORA-01034: ORACLE not available
ORA-27101: shared memory realm does not exist
Linux-x86_64 Error: 2: No such file or directory
Process ID: 0
Session ID: 0 Serial number: 0
````

解决方法为重启，原因不明：

```sh
/etc/init.d/oracle-xe disable
/etc/init.d/oracle-xe enable
/etc/init.d/oracle-xe start
```

### Linux ORA-12541: No Listener

曾因为修改了Hostname而触发此问题。

可以先重新配置`listener.ora`，然后重新启动监听器。

```sh
lsnrctl status
```

```conf
# listener.ora Network Configuration File:

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (SID_NAME = PLSExtProc)
      (ORACLE_HOME = /u01/app/oracle/product/11.2.0/xe)
      (PROGRAM = extproc)
    )
  )

LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC_FOR_XE))
      (ADDRESS = (PROTOCOL = TCP)(HOST = 0.0.0.0)(PORT = 1521))  # 可以将此处的HOST配置成0.0.0.0
    )
  )

DEFAULT_SERVICE_LISTENER = (XE)
```

```sh
lsnrctl start
lsnrctl status
```
