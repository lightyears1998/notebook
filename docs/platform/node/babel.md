# Babel

JavaScript编译器。

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

## 使用preset-env

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

---

- [Docs](https://babeljs.io/docs/en/)
