# C++基础

## 命名规范

| 风格         | 范围               |
| ------------ | ------------------ |
| `PascalCase` | 全局变量、函数、类 |
| `camelCase`  | 局部变量           |
| `snake_case` | 文件名 |

## 基本数据类型

- 在`climits`和`cfloat`头文件中定义了整型和浮点型的值域信息。

### `sizeof()`

1. `sizeof()`以字节为单位给出类型的内存大小。
2. `sizeof()`的返回值是一个`size_t`类型，它可能是`unsigned int`或`unsigned long`的同义词
3. 使用`printf()`打印`sizeof()`运算结果时，可以使用`%zd`或`%zx`等说明符。

```cpp
printf("Long类型的占用%zd字节。", sizeof(long));
```

### 整型 `short`, `int`(`long`), `long long`

| 整数字面值 | 数据类型             |
| ---------- | -------------------- |
| 32         | `int`                |
| 32L        | `long`               |
| 32LL       | `long long`          |
| 32U        | `unsigned int`       |
| 32UL       | `unsigned long`      |
| 32ULL      | `unsigned long long` |

| 浮点数字面值     | 数据类型 | 备注                                                         |
| ---------------- | -------- | ------------------------------------------------------------ |
| 32.64, .32, 0.32 | `double` | 默认情况下浮点数字面值总是被当作double类型。                 |
| 32.F             | `float`  | 只有使用F后缀的字面值才被当作float类型。                     |
| 3.2e3            | `double` | 值为`3.2 × 10³`                                              |
| 0xA.BCp10        | `double` | 十六进制浮点数，十进制值为`(10 × 16⁰ + 11 × 16⁻¹ + 12 × 16⁻² ) × 2¹⁰`。 |

注：

1. 没有八进制浮点数。
2. 对于十六进制浮点数，幂采用以**2为底的十进制数**。

#### 整型进位制

| 进位制                      | 前缀     | 例子                |
| --------------------------- | -------- | ------------------- |
| 十进制（**DEC**imal）       | N.A.     | `12`                  |
| 八进制（**OCT**al）         | `0`        | `014`，等于十进制数12 |
| 十六机制（**HEX**adecimal） | `0x` 或 `0X` | `0xC`，等于十进制数12 |

### 字符型 `char`

| 字面值                   | 类型                                         | 字符 |
| ---------------------- | ------------------------------------------------------ | --------------------------------------- |
| `99`, `0143` 或 `0x63` | 整型数值                                               | c                                       |
| `'c'`                  | 字符字面值                                             | c                                       |
| `'\n'`                 | 转义字符                                               | （换行）                                |
| `'\0143'` 或 `'\143'`  | 转义字符，格式为`\0ooo`或`\ooo`（其中`ooo`为八进制数） | c                                       |
| `'\x63'` 或 `'\0x63'`  | 转义字符，格式为`\xhh`，其中`hh`为十六进制数           | c                                       |

字符转义序列：

- 八进制字符 `\ooo`
- 十六进制字符 `\xhhh`
- Unicode字符 `\u00000000`

#### 宽字符类型 `wchar_t`、`char16_t`和`char32_t`

```cpp
wchar_t bob = L'P';
wcout << L"tall" << endl;  // 宽字符常量和宽字符串L前缀

char16_t ch1 = u'q';
char32_t ch2 = U'\U0000222B';
```

注：

- 在MSVC编译器里，`wchar_t`是UTF-16LE字符（Windows平台原生字符），`char16_t`是UTF-16字符，`char32_t`是UTF-32字符。

### 字符串类型 `cstring`(Null Terminated String)

字符串以空字符（'\0'）结束。在使用`scanf()`读取字符串以及使用字符串字面值，以及使用`printf()`打印字符串时，空字符会被自动处理。

#### 原始字符串

默认定界符 `R"(... )"`

自定义定界符可在默认定界符之间加入除空格、括号、斜杠、控制字符（制表符等）之外的任意字符。
例如 `R"delimiter(... )delimiter"`

### 强制类型转换

```cpp
(type)name
type(name)

static_cast<type>(name)
```

## 复合数据类型

列表初始化数组时可以省略等号，可不在大括号内包含任何东西即可将所有元素置零。

### 位字段

```cpp
struct torgle_register
{
    unsigned int SN: 4;
    unsigned int   : 4;  // 不使用的位
    bool goodIn    : 4;
    bool goodTorgle: 4;
};
```

### 共用体/联合 `Union`

匿名共用体：

```cpp
struct widget
{
    char brand[20];
    int type;
    union
    {
        long id_num;
        char id_char[20];
    }
}
```

### 枚举

枚举类型可用于创建符号常量（新的类型名和枚举量），可用枚举来定义switch语句中的符号常量。

定义的符号常量在枚举的作用域内有效。

```cpp
enum spectrum {red, orange, yellow, green, blue, violet, indigo, ultraviolet};

spectrum band = spectrum(3);  // green
spectrum band = green;
```

可以创建多个值相同的枚举量

每个枚举都有取值范围，可以将枚举变量中的任何整数值赋给枚举变量，即使这个值不是枚举值。

枚举的取值范围的计算：开区间，(min(比最小枚举值小的最大的2的幂次, -1), 比最大枚举值大的最小的2的幂次)
