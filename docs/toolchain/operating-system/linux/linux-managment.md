# Linux系统管理

## 基础信息

```sh
$ uname -r [-h]
3.10.0-957.27.2.el7.x86_64
```

## 在系统/终端启动时运行脚本

- `~/.bash_profile`
- `/etc/profile`或`/etc/profile.d/*.sh`

## Systemctl

```sh
systemctl
systemctl enable
systemctl disable
systemctl mask

journalctl -u [service-name]
```

## Mailing

以下设置可以连接到第三方服务器。编辑`/etc/mail.rc`，并授予需要发送邮件的用户以读权限。

```conf
# Connect to Aliyun Enterprise Mailing System.
set nss-config-dir=/etc/pki/nssdb/
set ssl-verify=ignore
set smtp=smtps://smtp.qiye.aliyun.com:465
set from=user@host
set smtp-auth-user=user@host
set smtp-auth-password=password
set smtp-auth=login
```

## Crontab

```sh
*min *hour *day *month *weekday0to6 /path/to/script >> /path/to/script.log 2>&1
```

## 自定义SSH欢迎文本

- tty `/etc/issue` `man issue` `man getty`
- Message of Today `etc/motd`

## 用户管理

```sh
whoami
groups [username]
cat /etc/passwd
cat /etc/group
cat /etc/sudoers

useradd <usrname>
passwd <usrname>
usermod <usrname> # Modify user
userdel [-r] <usrname>
```

## 磁盘管理

```sh
df -h
du [filename] [-sh] # Disk Usage
```

### 创建Swap文件

<https://linuxize.com/post/create-a-linux-swap-file/>

## 网络

```sh
export http_proxy=127.0.0.1:1080
export https_proxy=127.0.0.1:1080
```
