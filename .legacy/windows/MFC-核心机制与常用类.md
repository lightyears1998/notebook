# MFC核心机制与常用类

- [鸡啄米MFC教程](http://www.jizhuomi.com/catalog.asp?tags=MFC)

## 核心机制

1. MFC初始化
2. 运行时类型识别RTTI
3. 动态创建
4. 串行化
5. 消息映射和命令传递

## 常用类

### CWinApp

可以修改应用程序的名字

### CArchive

串行化神器。

使用示例

```cpp
CFile file;
file.Open(L"data.bin", CFile::modeCreate | CFile::modeReadWrite);
CArchive ar1(&file, CArchive::store);

ar1.WriteObject(&s1);
ar1.WriteObject(&s2);
ar1.WriteObject(&manager);
ar1.Close();

/* ====== */

file.SeekToBegin();
CArchive ar2(&file, CArchive::load);
Student * s = (Student*)ar2.ReadObject(RUNTIME_CLASS(Student));
Management * man = (Management*)ar2.ReadObject(RUNTIME_CLASS(Management));

```

### CString

有`CStringA`的变体

方法

- `CString(char *)` 由`char *`构造对象
- `Format()` 与printf()类似的格式化字符串的方法；由字符串转换成数值可以使用`atoi()`
- `GetBuffer()` 返回`char *`，此方法作为`std::string`与`CString`转换的桥梁

### CPoint, CSize, CRect

### CPaintDC

### CFile

有`CStdioFile`的子类支持文件输出

创建文件的模式 `CFile::modeXXX`

使用`Write()`正确地输出`CString`的方法 `Write(str.GetBuffer(), sizeof(TCHAR) * str.GetLength());`

### CStdioFile

本质上是对C的函数`fopen()`对应结构的封装，封装了`WriteString()`和`ReadString()`方法，注意两个版本的`ReadString()`对换行符的不同处理；

### CImageList

1. 创建图片集合

```cpp
CImageList list;
list.Create(...);  // 创建（开辟空间）
list.Add(...);  // 添加具体的图像，可以是HICON
