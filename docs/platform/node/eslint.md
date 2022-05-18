# ESlint

JS/TS 代码格式化工具。

``` sh
yarn add eslint --dev

yarn add @typescript-eslint/parser --dev
yarn add @typescript-eslint/eslint-plugin --dev

yarn add eslint-plugin-import --dev
```

``` sh
# 已包含 TypeScript 支持
eslint --init
```

``` sh
eslint src --ext .ts --fix
```

## 常用 `.eslintrc.yml`

- [eslint-config-lightyears-style](https://github.com/lightyears1998/eslint-config-lightyears-style)

``` yml
root: true
env:
  es6: true
  # node: true
  # browser: true
parser: '@typescript-eslint/parser'
parserOptions:
  project: ./tsconfig.json
plugins:
  - '@typescript-eslint'
  - import
extends:
  # react-app
  # plugin:@typescript-eslint/recommended
  - plugin:import/errors
  - plugin:import/warnings
  - plugin:import/typescript
  - "@lightyears1998/lightyears-style"
globals:
  Atomics: readonly
  SharedArrayBuffer: readonly
rules:
  indent:
    - warn
    - 2
    - SwitchCase: 1
  no-console:
    - off
```

## VS Code 设置 `settings.json`

``` json
{
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "editor.formatOnSaveMode": "modifications",
  "javascript.format.enable": false,
  "typescript.format.enable": false
}

```
