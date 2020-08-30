# GPG与SSH

## GPG - GnuPG

### 密钥对生成

``` sh
gpg gen-keys
```

### 密钥对导入导出

1. 将全部密钥对导出到远程机器

    ```sh
    scp -r ~/.gnupg user@remotehost:~/
    ```

2. 单密钥对的导出

    ```sh
    gpg --list-key
    gpg --output mykey_pub.gpg --armor --export 26D4F2F9
    gpg --output mykey_sec.gpg --armor --export-secret-key 26D4F2F9

    scp mykey_pub.gpg mykey_sec.gpg user@remotehost:~/

    gpg --import mykey_pub.gpg
    gpg --allow-secret-key-import --import mykey_sec.gpg
    ```

## SSH

默认位置 `~/.ssh/`，使用`ssh-keygen`生成密钥对。

### 客户端连接设置

```conf
# Read more about SSH config files: https://linux.die.net/man/5/ssh_config

ServerAliveInterval 60

Host qfstudio
    HostName qfstudio.net
    User username

Host node0.qfstudio
    HostName node0.qfstudio.net
    User lightyears

```

### 使用密钥对登陆

允许用户使用密钥对登录。

```conf
# /etc/ssh/sshd_config
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```

将公钥复制到服务器上。

```sh
ssh-copy-id user@host

# 亦可手动将公钥复制到`~/.ssh/authorized_keys`。
scp ~/.ssh/id_rsa.pub user@host:~/.ssh/uploaded_key.pub
ssh user@host
cat ~/.ssh/uploaded_key.pub >> ~/.ssh/authorized_keys

# 确保目录权限正确。
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

禁用密码登录。

``` shell
# Forbid users in group `forbidpasswdlogin` from logging in with password
Match User lightyears
    PasswordAuthentication no

Match Group forbidpasswdlogin
    PasswordAuthentication no
```

---

## Trouble shooting

### Windows: `warning: agent returned different signature type ssh-rsa (expected rsa-sha2-512)`

Windows的OpenSSH版本太旧。<https://github.com/PowerShell/Win32-OpenSSH/issues/1263>

### macOS：无法签名

可参照[这里提到的方案](https://stackoverflow.com/questions/39494631/gpg-failed-to-sign-the-data-fatal-failed-to-write-commit-object-git-2-10-0)解决。

### SSH 连接：GPG-Agent 不提示输入密码

原因：GPG-Agent 不明确应在哪个 TTY 要求用户输入密码。

解决方案：<https://gpgtools.tenderapp.com/kb/faq/enter-passphrase-with-pinentry-in-terminal-via-ssh-connection>

```sh
# ~/.zshrc
# For zsh, the following script should be placed in ~/.zshrc rather than ./zprofile

export GPG_TTY=$(tty)
if [[ -n "$SSH_CONNECTION" ]] ;then
    export PINENTRY_USER_DATA="USE_CURSES=1"
fi
```
