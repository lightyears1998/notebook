# C++笔记：语句

## 顺序语句

### `sizeof()`

`sizeof()`以字节为单位给出类型的大小，使用`printf()`打印`sizeof()`运算结果时，可以使用`%zd`或`%zx`等说明符。

`sizeof()`的返回值是一个`size_t`类型，它可能是`unsigned int`或`unsigned long`的同义词。

```c
printf("Long类型的占用%zd字节。", sizeof(long));
```
