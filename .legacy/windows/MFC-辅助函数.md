# MFC中常用的辅助函数

辨识方法

- Visual Studio 类视图
- 以`Ex`开头是拓展函数
- 以`AFX`开头的是全局函数；一个例子是`MessageBox()`是CWnd的方法，而`AfxMessageBox()`

宏

- `HIBYTE()`, `LOBYTE()` 16位数值中的高位和低位
- `TEXT()` UNICODE字符支持
- `MAKEWORD()` 将两个16数值合成32位数值

字符串处理

- `TCHAR` 自适应编码转换字符
- wchar_t配套方法`wcslen()`

窗口相关

- `ScreenToClient(&pt)` 窗口坐标到客户区域坐标的转变

基于对话框的程序

- 处理键盘输入<https://blog.csdn.net/wwkaven/article/details/39935915>
