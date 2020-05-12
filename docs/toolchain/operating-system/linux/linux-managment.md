# Linux系统管理

## 基础信息

```sh
$ uname -r [-h]
3.10.0-957.27.2.el7.x86_64

vi /etc/motd
/etc/update-motd.d
```

## Locale

- 在`/etc/locale.gen`中取消`zh_CN UTF8`的注释；`locale-gen`；`locale -a`。
- `localectl set-locale LANG=zh_CN.utf8`

## Date and Time

``` sh
timedatectl
```

## 在系统/终端启动时运行脚本

- `~/.bash_profile`, `~/.zshrc`
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

```sh
# 创建 Swapfile

sudo fallocate -l 2GiB /swapfile
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile

# 在 `/etc/fstab` 中可固化设置。
# `/swapfile swap swap defaults 0 0`
```

```sh
# swappiness 值在 [0, 100] 之间；值越高，系统越乐于使用交换分区。
# 默认值是 60，在现代硬件环境下使用 10 便足够。
cat /proc/sys/vm/swappiness

sudo sysctl vm.swappiness=10 # 临时修改
# 在 `/etc/sysctl.conf` 中可固化设置。
# `vm.swappiness=10`
```

```sh
# 移除 Swapfile 步骤

sudo swapoff -v /swapfile
# 从 `/etc/fstab` 中删除 `/swapfile swap swap defaults 0 0`。
sudo rm /swapfile
```

## 网络

```sh
export http_proxy=127.0.0.1:1080
export https_proxy=127.0.0.1:1080
```
