# Redis

以下指令都是 Redis 的原子操作。

对于 Redis，大多数结构在使用时不需要被显式地创建。

## 字符串操作

``` sh
SET ns:key "value"
GET ns:key
EXISTS ns:key
DEL ns:key
```

## 数值操作

``` sh
SET ns:key 10
INCR ns:key     # 即便 `ns:key` 不存在，INCR 操作也会创建一个，并返回 1
INCRBY ns:key 9
DECR
DECRBY
```

## 过期时间

``` sh
EXPIRE ns:key 120  # 120 秒后过期
TTL ns:key         # 返回剩余几秒后过期，-1 代表用户过期，-2 代表键不存在

# 不带参数的 SET 会重置过期时间，可以使用 EX 指定过期时间。
SET ns:key "value" EX 5

PERSIST ns:key  # 移除过期时间限制
```

## 列表操作

从这里继续：<https://try.redis.io/>
