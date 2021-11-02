# Go 工具

## `strings`

`strings.Join()`

## `os`

`os.Args`

## 进阶数据结构

### `Map`

Map不排序：处于Debug考虑，防止代码依赖某种特定的序列。

## 常用算法工具

### Sort

Go 的 Sort 接口 Not so easy。

``` go
func distributeCandies(candyType []int) int {
    sort.Slice(candyType, func(i, j int) bool {
        return candyType[i] < candyType[j]
    })

    ans := 0
    prev := int(1e7)
    for _, v := range candyType {
        if prev != v {
            ans++
            prev = v
        }
    }

    if ans < len(candyType)/2 {
        return ans
    }
    return int(len(candyType) / 2)
}
```
