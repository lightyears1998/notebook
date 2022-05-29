# 日期和时间

```py
import time
import datetime
```

- `time.time()` 生成当前时间的Linux时间戳

## `datetime.datetime`类

构造函数

1. `fromtimestamp()` 把时间戳解释成一个本地时区的datetime对象
2. `utcfromtimestamp()` 把时间戳解释成本地时区的datetime对象，并将此对象转换成UTC时间
3. `strptime(时间字符串, 格式字符串)`

```py
now = time.time()
local = datetime.datetime.fromtimestamp(now)
utc = datetime.datetime.utcfromtimestamp(now)
print(local, utc, sep='\n')  # 数值上UTC比本地时间（UTC+8）少8小时

"""
2018-10-15 19:08:10.914724
2018-10-15 11:08:10.914724
"""
```

## `strptime()` Parse a string to achieve a datetime object

```py
utc   = '2018-10-08T06:23:34.000Z'  # 这样的格式或许在写JS的时候是比较常见的
local = '2018-10-08 14:23:34'       # 正常人用的时间格式 🤦‍

datetime.datetime.strptime(utc, '%Y-%m-%dT%H:%M:%S.%fZ')  # %y是两位数的年份，%f微秒左侧第一位为最高位
datetime.datetime.strptime(local, '%Y-%m-%d %H:%M:%S')
```

## `strftime()` Generate a formatted time string

类型说明符与`strptime()`保持一致

## UTC时间与本地时间的互相转换

1. 借助`timestamp`

```py
def utc2local(utc: datetime.datetime):
    now = time.time()
    offset = datetime.datetime.fromtimestamp(now) - datetime.datetime.utcfromtimestamp(now)
    return utc + offset


def local2utc(local: datetime.datetime):
    now = time.time()
    offset = datetime.datetime.utcfromtimestamp(now) - datetime.datetime.fromtimestamp(now)
    return local + offset


timestamp = time.time()
local = datetime.datetime.fromtimestamp(time.time())
print('本地时间戳', timestamp)
print('本地时间', local)
print('UTC时间', local2utc(local))
print('本地时间（验证）', utc2local(local2utc(local)))


"""
本地时间戳 1539603479.3487046
本地时间 2018-10-15 19:37:59.348705
UTC时间 2018-10-15 11:37:59.348705
本地时间（验证） 2018-10-15 19:37:59.348705
"""
```
