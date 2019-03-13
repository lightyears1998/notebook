# Express

`app.use()`

use 对特定路径使用中间件

```js
app.use('path', (req, res, next) = > {
  next();
});
```

## bodyParser

```js
const bodyParser = require('body-parser');

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
```
