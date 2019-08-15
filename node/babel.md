# JavaScript编译器Babel

- [Docs](https://babeljs.io/docs/en/)

## 安装

```sh
npm install --save-dev @babel/core @babel/cli
```

package.json

```json
"scripts": {
  "build": "babel src -d lib"
},
```

## 环境预设

```sh
npm install --save-dev @babel/preset-env
```

.babelrc

```json
{
  "presets": [
    ["@babel/preset-env", {
        "targets": "> 0.25%, not dead"
      }
    ]
  ]
}
```
