# Git

- 在Windows环境下可与Kleopatra配合使用以取得GPG支持。

## 起飞操作

1. `git init`
2. gitignore
3. gitattributes

## 常用设定

```sh
git config --global "user.name" "lightyears1998"
git config --global "user.email" "lightyears1998@hotmail.com"
git config --global "core.ignorecase" false
```

### 对换行符的处理

不推荐使用`core.autocrlf`方式。

```sh
git config --global "core.autocrlf" true # Windows
git config --global "core.autocrlf" input # Linux, MacOS
git add --renormalize
```

推荐使用[`.gitattributes`](https://help.github.com/cn/github/using-git/configuring-git-to-handle-line-endings)

```txt
# Set the default behavior, in case people don't have core.autocrlf set.
* text=auto

# Explicitly declare text files you want to always be normalized and converted
# to native line endings on checkout.
*.c text
*.h text

# Declare files that will always have CRLF line endings on checkout.
*.sln text eol=crlf

# Denote all files that are truly binary and should not be modified.
*.png binary
*.jpg binary
```

## GPG相关

```sh
git config --global "commit.gpgsign" true
git config --global "gpg.program" "C:\Program Files (x86)\GnuPG\bin\gpg.exe"
git config --global "user.signingkey" "26D4F2F9"
```

## 操作

```sh
git push <repo> <from-local-branch>:<to-remote-branch>
git pull <repo> <from-remote-branch>:<to-local-branch>
```

```sh
git pull --force <repo> <some-remote-branch>:<to-local-branch>  # 拉取并覆盖本地更改
git push <remote-name> --delete <remote-branch> # 删除远程分支

# 从远程分支处继续工作
git checkout -b <repo>/<remote-branch>
git branch -m <new-name>
git push --set-upstream <repo> <remote-branch>
```

## 标签

```sh
git tag
git tag -a "标签信息" [-m "message"] [commit-sha1]
git push <remote> --tags
```
