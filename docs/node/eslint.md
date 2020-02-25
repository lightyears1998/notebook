# ESlint

JavaScript / TypeScript的格式化工具。

```sh
yarn global add eslint
eslint --init  # 自定义配置

eslint src --ext .ts --fix
```

## `.eslintrc.yml`

- 泛用性 <https://github.com/lightyears1998/code-sandbox/blob/master/node/eslint/general.yml>
- 风格化 <https://github.com/lightyears1998/code-sandbox/blob/master/node/eslint/style.yml>

## VS Code拓展全局设置

```json
{
    "eslint.experimental.incrementalSync": true,
    "eslint.autoFixOnSave": true,
    "eslint.lintTask.enable": true,
}
```
