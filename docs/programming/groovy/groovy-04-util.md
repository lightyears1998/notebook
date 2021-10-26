# Groovy 工具

## 进阶数据结构

### 集合`Set`

- 定义集合 `` ArrayList
- 转换集合 `` `as`用于转换兼容集合

```groovy
def nums = [1, 1, 2, 3, 5]  // java.util.ArrayList
Set uniques = nums as Set   // `as`用于进行兼容转换
```

### 映射`Map`

```groovy
def map = [a:1, b:2, c:3]

map.a
map['b']
map.get('c')
```
