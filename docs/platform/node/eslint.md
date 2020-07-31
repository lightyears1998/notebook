# ESlint

JS/TS 代码格式化工具。

``` sh
yarn add eslint --dev

yarn add @typescript-eslint/parser --dev
yarn add @typescript-eslint/eslint-plugin --dev

yarn add eslint-plugin-import --dev
```

``` sh
eslint --init
```

``` sh
eslint src --ext .ts --fix
```

## 常用 `.eslintrc.yml`

- [eslint-config-lightyears-style](https://github.com/lightyears1998/eslint-config-lightyears-style)

``` yml
env:
  es6: true
  # node: true
  # browser: true
parser: '@typescript-eslint/parser'
parserOptions:
  project: ./tsconfig.json
plugins:
  - import
extends:
  # react-app
  # plugin:@typescript-eslint/recommended
  - plugin:import/errors
  - plugin:import/warnings
  - plugin:import/typescript
  - "@lightyears1998/lightyears-style"
rules:
  import/order:
    - warn
```

## VS Code拓展全局设置

```json
{
    "eslint.experimental.incrementalSync": true,
    "eslint.autoFixOnSave": true,
    "eslint.lintTask.enable": true,
}
```
