# Express

`app.use()` 对特定路径使用中间件

```js
app.use('path', (req, res, next) = > {
  next();
});
```

## bodyParser

用于解析Body部分的结构化数据，如JSON等。

```js
const bodyParser = require('body-parser');

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
```
