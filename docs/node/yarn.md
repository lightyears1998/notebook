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
