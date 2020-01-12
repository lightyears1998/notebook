# HTTP请求

- 使用`requests`。

## requests

## 使用urllib中的request

- [Python Docs](https://docs.python.org/3/library/urllib.html)

```py
from urllib import request

url = 'http://www.baidu.com'
with request.urlopen(url) as f:
    print(f.read())
```
