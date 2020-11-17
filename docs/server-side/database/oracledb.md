# Oracle数据库笔记

## 常识

### 单引号与双引号

- **双引号** 建立对象时，将对象名、字段名等加双引号，Oracle将严格区分大小写，否则都默认为大写。
- **单引号** 字符串；两个单引号表示跳脱，用于表示一个单引号字符。

在单引号字符比较多的情况下可以使用Literal Quoting，形如`q'['泛人类史'大纲]'`。

```sql
-- 注意到IDENTIFIED BY字句的参数"password"必须使用双引号或不使用引号（即使不使用双引号也是大小写敏感的），
-- 而使用单引号则会报错。
CREATE USER "username" IDENTIFIED BY "password";
```

### SID名称

```sql
select instance from v$thread;
```

Express版本的默认SID是`xe`，企业版的默认SID是`orcl`。

### Oracle National Language Support

```sql
SELECT * FROM nls_database_parameters ORDER BY PARAMETER;
```

此查询会给出数据库字符集等信息。

### 字符集

NVARCHAR2(10)与VARCHAR2(10 CHAR)的储存能力是相同的。

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

此方法通用性较高，网络上存有较多文档。
