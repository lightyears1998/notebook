# NPM与NPX

Node Project Manager & Npm package runner

## 包管理

- 列出配置 `npm config list`

    global package安装于`npm config get prefix`所给出的`{prefix}/node_modules`目录中, local package安装于当前工作路径。global包位于PATH中，通常是CLI工具。

- 安装包 `npm install <package-name>`，使用`--global`或`-g`进行全局安装。
  - 使用`package-name@major.minor.patch`来指定版本。
  - 使用`--no-save`而不将信息保存到`package.json`
- 列出包 `npm list [--global | -g]`，使用`--depth=0`来指定列出包的深度。
- 卸载包 `npm uninstall <package-name>`
- 列出潜在升级 `npm outdated`或`npm outdate`
- 执行升级 `npm update [package-name]`
- 修正安全问题 `npm audit`
- 搜索包 `npm search`

## 工作目录中的包管理

- `npm init`，使用`-y`快速生成。
- 开发时依赖`devDependency` `--save-dev`
- 对于私有软件可在`package.json`声明`private: true`。
- 在`package.json`中，包版本号前的`^`表示指主版本号相符的最新包，即下一个主版本前的最新包。

## 维护

- 清理缓存 `npm cache clean`

---

## 安装与更新

建议随Node一同更新。

在Linux上执行`npm install npm@latest -g`。

在Windows不能直接执行上述命令，而需要[`npm-windows-upgrade`](https://www.npmjs.com/package/npm-windows-upgrade)工具。

## 镜像

参考淘宝NPM镜像使用CNPM。

临时使用

```sh
npm install <package-name> --registry https://registry.npm.taobao.org
```

持久使用（不推荐，应使用CNPM）

```sh
npm config set registry https://registry.npm.taobao.org
```
