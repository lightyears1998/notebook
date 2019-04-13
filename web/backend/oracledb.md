# Oracle数据库笔记

## 常识

## 数据安全性

通过创建角色来管理权限。

```sql
CREATE ROLE 角色名;
GRANT 权限名 TO 角色名;

GRANT 角色名 TO 用户名;
```

已经连接的用户被授予了新角色时，仍是以旧角色的权限进行连接；若要使用新角色的身份，可以重新连接，或者使用`SET ROLE 新角色名;`来刷新权限。

## PL/SQL

- 使用`EXEC IMDEIDATE 'SQL语句';`时，SQL语句不能加入分号。

## 编程语言集成

### Oracle专用方法

- **OCI** *Oracle Call Interface* C语言的Oracle调用库，也是开发其他调用库的基础；OCI被包含在Oracle数据库的安装选项中，但若要使用OCI进行开发，则使用Instant Client更为方便
- **OCCI** *Oracle C++ Call Interface* C++形式的Oracle调用库，
- **Instant Client** 基础组件包含了运行OCI/OCCI所必须的文件，需要跟随OCCI应用程序一起部署到目标机器；SDK部分包含进行开发时需用的头文件和调试版本的库

### ODBC *Open DataBase Connection* 跨平台跨数据库通用方法

此方法通用性较高。
