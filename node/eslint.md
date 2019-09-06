# ESlint

```sh
npm install eslint --save-dev
eslint --init  # 自定义配置
```

## 一般用途`.eslintrc.yml`

```yml
env:
  browser: true
  commonjs: true
  es6: true
  node: true
extends:
  - 'eslint:recommended'
globals:
  Atomics: readonly
  SharedArrayBuffer: readonly
parserOptions:
  ecmaVersion: 2018
rules:
  brace-style:
    - warn
    - 1tbs
  curly:
    - warn
    - all
  dot-location:
    - warn
    - object
  dot-notation:
    - warn
  eqeqeq:
    - warn
    - smart
  indent:
    - warn
    - 2
  linebreak-style:
    - warn
    - unix
  no-trailing-spaces:
    - warn
  no-else-return:
    - warn
  no-implicit-coercion:
    - warn
  no-multi-spaces:
    - warn
    - {
      ignoreEOLComments: true
    }
  no-return-await:
    - warn
  wrap-iife:
    - warn
    - inside
  quotes:
    - warn
    - single
  semi:
    - warn
    - never
  yoda:
    - warn
    - never
  block-spacing:
    - warn
    - always
  camelcase:
    - warn
    - {
      properties: always,
      ignoreDestructuring: false,
      allow: []
    }
  comma-dangle:
    - warn
    - never
  comma-spacing:
    - warn
    - {
      before: false,
      after: true
    }
  comma-style:
    - warn
    - last
  eol-last:
    - warn
    - always
  func-call-spacing:
    - warn
    - never
  jsx-quotes:
    - warn
    - prefer-double
  key-spacing:
    - warn
    - {
      beforeColon: false,
      afterColon: true,
      align: value
    }
  keyword-spacing:
    - warn
    - {
      before: true,
      after: true
    }
  new-parens:
    - warn
    - always
  no-lonely-if:
    - warn
  multiline-comment-style:
    - warn
    - starred-block
  no-whitespace-before-property:
    - warn
  object-curly-spacing:
    - warn
    - always
  array-bracket-spacing:
    - warn
    - never
  space-before-blocks:
    - warn
    - always
  space-before-function-paren:
    - warn
    - {
      anonymous: always,
      named: never,
      asyncArrow: always
    }
  space-in-parens:
    - warn
    - never
  spaced-comment:
    - warn
    - always
  switch-colon-spacing:
    - warn
    - {
      before: false,
      after: true
    }
  template-tag-spacing:
    - warn
    - never
  unicode-bom:
    - warn
    - never
  wrap-regex:
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
