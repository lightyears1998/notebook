# C++ 工具

## 输入输出工具

### `cin`

- `getline(buf, num)` 丢弃换行符
- `get(buf, num)` 换行符留在输入队列中
- `get()` 读取一个字符
- `clear()`
- `fail(), eof()` 检测到EOF后，cin的failbit和eofbit都置1；

get()（不是getline()）读取空行后设置失效位(failbit)，需要使用`cin.clear()`恢复。

get(), getline()输入行的字符比指定容量多时，将设置失效位

```cpp
cin.get(name, ArSize).get();
```

### 宽字符输出 `cout`, `wcout`

- `put()`
- `setf(ios_base::fixed, ios_base::floatfield);`

### IO符号 `flags`

- `setioflags(ios_base::fixed|ios::showpoint)`
- `setprecision(2)`

### 文件IO `fstream`

```cpp
ofstream fout = open(name);
fout.close();
```

### IO格式更改与恢复

```cpp
fmtflags fmt = cout.flags();
cout.flags(fmt);
```

## 进阶数据结构

### `std::vector`, `std::array`

中括号语法不检查下标越界，成员函数`at()`检查下标越界

### `std::map`, `std::unordered_map`

- `find()`
- `count()`, `contains()`
