# C++ 语句

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

## 异常控制

头文件 `<stdexcept>`
