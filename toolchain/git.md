# Git

在Windows环境下可与Kleopatra配合使用。

常用设定：

```sh
git config --global "user.name" "lightyears1998"
git config --global "user.email" "lightyears1998@hotmail.com"
git config --global "core.ignorecase" false
git config --global "core.autocrlf" false
```

## GPG相关

```sh
git config --global "commit.gpgsign" true
git config --global "gpg.program" "C:\Program Files (x86)\GnuPG\bin\gpg.exe"
git config --global "user.signingkey" "26D4F2F9"
```

## 操作

```sh
git pull --force <repo> <remote-branch>:<local-branch>  # 拉取并覆盖本地更改
git push <remote-name> --delete <remote-branch> # 删除远程分支
```
