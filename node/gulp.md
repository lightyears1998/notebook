# Gulp

- [Docs](https://gulpjs.com/docs/en/getting-started/javascript-and-gulpfiles)

## 安装

```sh
yarn global add gulp-cli
yarn add --dev gulp
npx -p touch nodetouch gulpfile.js
gulp --help

# For gulpfile.ts
yarn add --dev typescript ts-node

# For gulpfiel.babel.js
yarn add --dev @babel/register
```

## 配置

1. 不`export`的task视为private task，不会直接被调用。
