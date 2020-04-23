# C#常识

```csharp
using System;

namespace HelloText
{
    class Program
    {
        public static void Main(String[] args)
        {
            Console.WriteLine("Hello, world!");
        }
    }
}
```

可以使用[命令行工具][]进行编译。

[命令行工具]: https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/compiler-options/command-line-building-with-csc-exe

## 基本常识

- **明确赋值原则** C#中不允许使用没有赋值的变量。
- **隐式类型变量** 相当于C++中的`auto`，使用`var`关键字。由编译器负责类型推断。

## 使用unsafe标记不安全的代码

使用`unsafe`时，需要在项目属性中设置允许不安全的代码

```cs
public static void Main(string[] args)
{
    int x = 99, y = 12;
    unsafe
    {
        Swap(&x, &y);
    }
}

public static unsafe void Swap(int *a, int *b)
{
    a ^= b;
    b ^= a;
    a ^= b;
}
```
