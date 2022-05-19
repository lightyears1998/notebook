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

虽然 ESLint 也可以作为代码格式化工具使用，但格式化的工作还是交给 prettier 吧。

理由：

- typescript-eslint 的 indent 规则由于[缺乏维护者](https://github.com/typescript-eslint/typescript-eslint/issues/1824)而不可使用。

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

在使用 TypeScript ESLint 时[需要](https://github.com/typescript-eslint/typescript-eslint/issues/1824)关闭原生 indent 规则。

不过，由于 TypeScript ESLint 的 indent 实现亦由于缺乏维护者而存在问题（例如无法正确处理 Decorators 的 indent。）Indent 应当交给 prettier。

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
