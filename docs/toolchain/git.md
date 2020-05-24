# Git

- 在Windows环境下可与Kleopatra配合使用以取得GPG支持。

## 起飞操作

1. `git init`
2. gitattributes `* text=auto`
3. gitignore 可使用<https://www.gitignore.io>创建

- commit的comment第一行为标题，采用行首单词首字母大写的格式。

## 常用设定

```sh
git config --global "user.name" "lightyears1998"
git config --global "user.email" "lightyears1998@hotmail.com"
git config --global "core.ignorecase" false

# Windows上无需此项，Git for Windows会自动使用Windows Credential Manager。
git config --global credential.helper <manager> # 见后文“保存凭证”小节

git config --unset key.name
```

GPG相关的设定：

```sh
git config --global "commit.gpgsign" true
git config --global "user.signingkey" "26D4F2F9"

# For Windows kleopatra
git config --global "gpg.program" "C:\Program Files (x86)\GnuPG\bin\gpg.exe"
```

### 保存凭证

1. 使用[libsecret](https://wiki.gnome.org/Projects/Libsecret)取代libgnome-keyring（注意不是取代gnome-keyring）。

   ```sh
    # 参考 https://askubuntu.com/a/959662

    sudo apt-get install libsecret-1-0 libsecret-1-dev libglib2.0-dev
    sudo make --directory=/usr/share/doc/git/contrib/credential/libsecret
    git config --global credential.helper \
        /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
   ```

### 对换行符的处理

使用`core.autocrlf`方式（不推荐）：

```sh
git config --global "core.autocrlf" true # Windows
git config --global "core.autocrlf" input # Linux, MacOS
git add --renormalize
```

使用[`.gitattributes`](https://help.github.com/cn/github/using-git/configuring-git-to-handle-line-endings)（推荐）：

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

### 网络代理

Git会无视系统代理设定，需要单独设置。推荐使用HTTPS代理而不是SSH代理。

```sh
git config --global http.proxy "socks5://127.0.0.1:1080"
git config --global https.proxy "http://127.0.0.1:1080"
```

SHH代理可参见。

## 常用指令

### 分支操作

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

### 打标签

```sh
git tag
git tag -a "标签信息" [-m "message"] [commit-sha1]
git push <remote> --tags
```

### 检查签名

```sh
git log --show-signature -1
```

---

- [Git/Github 中文术语表](https://mp.weixin.qq.com/s/5EvrlCVc7g0LX7DMhI-ZnQ)
