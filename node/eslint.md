# ESlint

```sh
npm install eslint --save-dev
eslint --init  # 自定义配置
```

## 个人配置

.eslintrc.yml

```yml
env:
  browser: true
  commonjs: true
  es6: true
  node: true
extends: 'eslint:recommended'
globals:
  Atomics: readonly
  SharedArrayBuffer: readonly
parserOptions:
  ecmaVersion: 2018
rules:
  brace-style:
    - error
    - 1tbs
  curly:
    - error
    - all
  dot-location:
    - error
    - object
  dot-notation:
    - error
  eqeqeq:
    - error
    - always
  indent:
    - error
    - 2
  linebreak-style:
    - error
    - unix
  no-trailing-spaces:
    - error
  no-else-return:
    - error
  no-implicit-coercion:
    - error
  no-multi-spaces:
    - error
    - {
      ignoreEOLComments: true
    }
  no-return-await:
    - error
  wrap-iife:
    - error
    - inside
  quotes:
    - error
    - single
  semi:
    - error
    - never
  yoda:
    - error
    - never
  block-spacing:
    - error
    - always
  camelcase:
    - error
    - {
      properties: always,
      ignoreDestructuring: false,
      allow: []
    }
  comma-dangle:
    - error
    - never
  comma-spacing:
    - error
    - {
      before: false,
      after: true
    }
  comma-style:
    - error
    - last
  eol-last:
    - error
    - always
  func-call-spacing:
    - error
    - never
  jsx-quotes:
    - error
    - prefer-double
  key-spacing:
    - error
    - {
      beforeColon: false,
      afterColon: true,
      align: value
    }
  keyword-spacing:
    - error
    - {
      before: true,
      after: true
    }
  new-parens:
    - error
    - always
  no-lonely-if:
    - error
  multiline-comment-style:
    - error
    - starred-block
  no-whitespace-before-property:
    - error
  object-curly-spacing:
    - error
    - always
  array-bracket-spacing:
    - error
    - never
  space-before-blocks:
    - error
    - always
  space-before-function-paren:
    - error
    - {
      anonymous: always,
      named: never,
      asyncArrow: always
    }
  space-in-parens:
    - error
    - never
  spaced-comment:
    - error
    - always
  switch-colon-spacing:
    - error
    - {
      before: false,
      after: true
    }
  template-tag-spacing:
    - error
    - never
  unicode-bom:
    - error
    - never
  wrap-regex:
    - error
```

## VS Code拓展全局设置

```json
{
    "eslint.experimental.incrementalSync": true,
    "eslint.autoFixOnSave": true,
    "eslint.lintTask.enable": true,
}
```
