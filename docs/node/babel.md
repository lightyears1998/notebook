# Babel：JavaScript编译器

- [Docs](https://babeljs.io/docs/en/)
- [Code-Sandbox](https://github.com/lightyears1998/code-sandbox/tree/master/node/babel)

## 安装

```sh
yarn add --dev @babel/core @babel/cli
```

package.json

```json
"scripts": {
  "watch": "babel src --out-dir lib --source-maps inline --watch",
  "build": "babel src --out-dir lib --source-maps inline"
},
```

## 环境预设

[Docs](https://babeljs.io/docs/en/babel-preset-env)

```sh
yarn add --dev @babel/preset-env
```

.babelrc

```json
{
  "presets": [
    [
      "@babel/preset-env", {
        "targets": "> 0.25%, not dead"
      }
    ]
  ]
}
```
