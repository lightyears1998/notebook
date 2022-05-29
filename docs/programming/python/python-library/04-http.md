# HTTP请求

使用`requests`。

## requests

```py
import requests

with requests.get(url) as response:
    response.encoding = 'gb2312' # 如有必要
    with open("../out/response.html", "w", encoding="utf8") as f:
        f.write(response.text)
    tree = etree.fromstring(response.text, etree.HTMLParser())
    print(tree.xpath('//*'))
```

## 使用urllib中的request

- [Python Docs](https://docs.python.org/3/library/urllib.html)

```py
from urllib import request

url = 'http://www.baidu.com'
with request.urlopen(url) as f:
    print(f.read())
```
