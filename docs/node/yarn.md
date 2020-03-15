# Yarn包管理器

```sh
yarn global add <package>

yarn install
yarn install --check-files  # 在手动删除Node Modules中的模块后重新安装。
yarn add [--dev] <package> [--registry https://r.npm.taobao.org]

yarn outdated
yarn upgrade
```

---

## 安装

- 根据[官网](https://yarnpkg.com/en/docs/install)上的指引进行安装；
- 在Windows上可以使用`choco`；
- 小心不要在Linux上使用包管理器安装错误的包。

```sh
yarn config set proxy http://host:port
yarn config set https-proxy http://host:port
```

## Per-Repo设置

如果要在`.yarnrc`中设置`registry`，最好也设置`.npmrc`；因为yarn可能会遵照npm的一些全局设置。

```conf
# .npmrc
registry=https://registry.npm.taobao.org

# .yarnrc
registry "https://registry.npm.taobao.org"
```

可以用`yarn config list`来检查这些设置是否生效。
