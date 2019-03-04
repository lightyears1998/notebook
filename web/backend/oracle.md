# Oracle相关注意事项

## 使用C/C++编程

### Oracle专用方法

- **OCI** *Oracle Call Interface* C语言的Oracle调用库，也是开发其他调用库的基础；OCI被包含在Oracle数据库的安装选项中，但若要使用OCI进行开发，则使用Instant Client更为方便
- **OCCI** *Oracle C++ Call Interface* C++形式的Oracle调用库，
- **Instant Client** 基础组件包含了运行OCI/OCCI所必须的文件，需要跟随OCCI应用程序一起部署到目标机器；SDK部分包含进行开发时需用的头文件和调试版本的库

### ODBC *Open DataBase Connection* 跨平台跨数据库通用方法

此方法通用性较高。

### 版本与兼容性问题

Instant Client的版本一般是向下兼容的，所以不需要为了连接Oracle 11g而使用版本11.2的Instant Client，使用现代的版本以配合现代的编译环境。

如果现在现代环境中使用旧版本的Instant Client，比如在VS2017中使用Instant Client 11.2，则需要注意：在调试时可能出现`MSVCR100.dll`缺失等由于VS1017无法安装v100平台工具集而无法正确解决的问题。（可以通过Dirty hack，在生成目录中放入`MSVCR100.dll`以使得程序不报错。）
