# Yarn包管理器

```sh
yarn global add <package>

yarn install
yarn install --check-files
# 有时候`--check-files`不管用；
# 需要手动删除`node_modules`后再运行yarn install。

yarn add [--dev] <package> [--registry https://r.npm.taobao.org]

yarn outdated
yarn upgrade [--latest] # `lastest` 会更新 package.json 中的版本
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
package-lock=false
registry=https://registry.npm.taobao.org


# .yarnrc
registry "https://registry.npm.taobao.org"
```

可以用`yarn config list`来检查这些设置是否生效。
