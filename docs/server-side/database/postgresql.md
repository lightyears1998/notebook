# PostgreSQL

## 管理

PostgreSQL可使用Linux用户身份对数据库进行管理，默认用户是`postgres`。

```sh
sudo -i -u postgres   # 切换为postgres身份
createuser <username> # 创建新用户，此时创建的用户不是Linux用户
createdb <dbname> -O <username> # 创建数据库并指定owner
psql                  # 进入控制台

\password <username>  # 设置密码
\q
exit # 退出postgres身份
```

```sh
# 验证密码设置
psql --host=localhost --dbname=DBNAME --username USERNAME --password
```

## 登陆

```sh
psql -U username -d dbname -h localhost -p 5432
```

## 常用控制台指令

```sh
\help # 常规SQL帮助
\?  # 控制台指令帮助
\l  # 显示所有数据库
\dt # 显示所有表
\c DB_NAME # 连接到数据库
```

---

## 安装

```sh
yum install postgresql-server postgresql-contrib
postgresql-setup initdb
systemctl start postgresql
systemctl enable postgresql
```

### 允许使用密码访问

编辑`pg_hba.conf`（`/var/lib/pgsql/data/pg_hba.conf`），使用MD5验证方式。（注意`password`方式是明文密码。）

```txt
# TYPE  DATABASE        USER            ADDRESS                 METHOD
host    all             all             127.0.0.1/32            md5
host    all             all             ::1/128                 md5
```

### 允许远程连接

编辑`pg_hba.conf`（`/var/lib/pgsql/data/pg_hba.conf`）中的地址字段，如果要允许所有IP访问，可将Address设置为`0.0.0.0/0`。

编辑`postgresql.conf`（`/var/lib/pgsql/data/postgresql.conf`），设置`listen_addresses = '*'`

如有必要，为`postgres`用户设置密码。

### 管理拓展

已安装“uuid-ossp”拓展为例。

``` sql
-- 必须以 SuperUser 身份执行
CREATE EXTENSION IF NOT EXISTS "uuid-ossp" WITH SCHEMA public;
```

## 客户端

- pgAdmin4 跨平台图形界面客户端。
