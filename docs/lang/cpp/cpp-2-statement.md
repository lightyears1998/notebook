# C++语句

## 表达式语句

### 声明

#### `new`与`delete`

- 使用`delete[]`释放`new[]`申请的内存
- 不要释放已经释放的内存
- 对空指针使用delete是安全的。

#### `new`

单值变量的列表初始化

```cpp
int *pin = new int{ 6 };
```

new失败时引发`std::bad_alloc`异常，在旧的标准中返回空指针。

#### 定位`new`运算符（placement new）

手动指定分配的内存起点，而不是在堆中自动管理。不跟踪已使用哪些内存，不能使用`delete`释放（因为`delete`只能释放自动分配的内存）。

```cpp
char buf[200];

int *p = new(buf) type_name;
```

## 循环语句

```cpp
// 延时循环
int sec; cin >> sec;
clock_t start = clock();
clock_t delay = sec * CLOCKS_PER_SEC;
while (clock() - start < delay) continue;
cout << "Done." << endl;
```

```cpp
// 范围循环
for (int x : {3, 5, 7, 9, 11})
{
    cout << x << endl;
}
```

## 异常处理语句

头文件 `<stdexcpet>`

---

另参见[C语言语句](../c/c-2-statement.md)。
