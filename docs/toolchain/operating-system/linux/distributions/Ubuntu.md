# Ubuntu

```
# 必备软件
sudo apt install gnome-tweaks
```

## apt

> The `apt` command is meant to be pleasant for end users and does not need
> to be backward compatible like `apt-get(8)`.

- 镜像 <https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/>
- 发行版版本 `lsb_release -a` `uname -r` `do-release-upgrade`
- `apt update`, `apt upgrade`, `apt search`, `apt list upgradable`

## 中文输入法

保持使用Ibus为宜。
使用RIME输入法。

```sh
sudo apt install ibus-rime
ibus-setup
```
