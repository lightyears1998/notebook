# Groovy 模块

## 闭包

### `each`方法

```groovy
def nums = [1, 2, 3, 4, 5]
def doubles = []

nums.each { n ->  // 箭头操作符
    doubles << n * 2
}

assert doubles == [2, 4, 6, 8, 10]
```

### `collect`方法

```groovy
def nums = [1, 2, 3, 4, 5]
def doubles = nums.collect { it * 2 }
assert doubles == [2, 4, 6, 8, 10]
```
