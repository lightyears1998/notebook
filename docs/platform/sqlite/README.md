# Sqlite

- [官网](https://www.sqlite.org/)
- [源码](https://sqlite.org/src/doc/trunk/README.md)
- [SQLite3 SQL 语言标准](https://www.sqlite.org/lang.html)

## 杂项

1. 用双引号逃脱特殊的标识符（标准 SQL）；同时也支持使用反引号（MySQL 转义符）和中括号（SQL Server 转义符）。
2. `INTEGER PRIMARY KEY AUTOINCREMENT` 与 `INT PRIMARY KEY` [不太一样](https://sqlite.org/lang_createtable.html#rowid)：`INTEGER PRIMARY KEY` 会重用 `rowid`。
