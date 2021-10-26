# C# 工具

## 输入输出工具

- `Console.WriteLine()`
- `Int.Parse()`

## 进阶数据结构

### `Dictionary`

``` csharp
var dict = new Dictionary<string, int>();

dict.Add("key", 0);
dict.ContainsKey("key");

int value = 0;
if (dict.TryGetValue("key", out value))
{
    // Got value.
} else {
    // Key doesn't exist.
}
```
