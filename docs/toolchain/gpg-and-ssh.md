# GPG与SSH

## GPG - GnuPG

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

1. 密钥对的生成 `ssh-keygen`
2. 默认位置 `~/.ssh/`
3. 使用密钥对登陆。

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
    ```

    确保目录权限正确

    ```sh
    chmod 700 ~/.ssh
    chmod 600 ~/.ssh/authorized_keys
    ```

---

## Troble shooting

### Windows: `warning: agent returned different signature type ssh-rsa (expected rsa-sha2-512)`

Windows的OpenSSH版本太旧。<https://github.com/PowerShell/Win32-OpenSSH/issues/1263>

### SSH连接：GPG-Agent不提示输入密码

原因：GPG-Agent不明确应在哪个TTY要求用户输入密码。

解决方案：<https://gpgtools.tenderapp.com/kb/faq/enter-passphrase-with-pinentry-in-terminal-via-ssh-connection>

```sh
export GPG_TTY=$(tty)
if [[ -n "$SSH_CONNECTION" ]] ;then
    export PINENTRY_USER_DATA="USE_CURSES=1"
fi
```
