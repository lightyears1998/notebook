# C# 语句

## 分支语句

bool类型的值是`true`和`false`

- `&&`和`||`都是短路运算符
- **C#只允许使用显式的布尔表达式** 不能在if后面的括号中使用数值表达式

```cs
if (boolExpression)
    statement;

switch (controllingExpression)
{
    case constantExpression:
    default:
}

while (boolExpression)
    statement;

for (init; controllingExpression; step)
    statement;

do {
    statement
} while (controllingExpression);
```

## 异常控制

形如Java

```cs
try
{
    something;
}
catch (Exception ex)
{
    dosomething;
}
finally
{
    finalJob;
}
```

### 异常过滤器

```cs
catch (Exception ex) when (ex.GetType() != typeof(System.OutOfMemoryException))
{
    // 捕捉OutOfMemory之外的异常
}
```

### `checked`和`unchecked`整数运算检查

也可以通过设置项目属性“高级生成设置”来手动启用溢出检查，不管项目如何编译，`checked`和`unchecked`总是覆盖项目的自动编译选项

```cs
checked{
    int number = int.MaxValue;
    checked
    {
        int willThrow = number++;
        Console.WriteLine("不会执行到这里");
    }
}
```

`checked`和`unchecked`只适用于浮点数

### 抛出异常

```cs
throw new ArgumentOutOfRangeException("不存在的月份");
```
