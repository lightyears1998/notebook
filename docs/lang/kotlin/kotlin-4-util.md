# Kotlin 工具

## 数据结构

### `Map`, `MutableMap`

``` kotlin
val map: MutableMap<Int, Int> = mutableMapOf(1 to 100, 2 to 100, 3 to 100)

map.forEach {
    k, v -> println("$k: $v")
}
```

- `containsKey(key)`
- `[key]`, `getValue(key)`
