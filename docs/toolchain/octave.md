# Octave笔记

[![code-sandbox](https://img.shields.io/badge/code--sandbox-29b7cb.svg)](https://github.com/lightyears1998/code-sandbox/blob/master/algorithm)

## 概述

与Matlab语法兼容的开源科学计算与数值分析工具。

具有CLI和GUI版本。

## 输入与输出

- 选择数值显示的方式：`format` `help format`
- 保存和读取工作环境/变量：`save <filename> [var1] [var2] [...]` `load <filename>`
- 在语句末尾使用分号 `;` 来隐藏计算结果回显。
- 保持语义的换行是`...`，不要在省略号后附加任何符号。可用于在多行内输入一个行变量（一维数组）。
- 分屏显示 `more <off / on>`
  - `space` 下一页
  - `b` 上一页
  - `q` 退出

## 基本概念

- 注释使用`#`或`%`。
- 数组的下标从1开始。
- 三角函数使用弧度制。
- 自然对数是`log`而不是`ln`。

## 变量

1. 变量区分大小写。
2. `who` 命令查看当前命名的函数和变量。
3. `clear [var-name]` 清除全部变量或特定变量。
4. `disp()` 显示字符串或变量的值。

## 数组和向量

- 构造向量
  - `a = [1 3 5]`
  - `b = [2, 4, 6]`
  - `c = [3; 6; 9]`
  - 逗号或空格隔开是行向量；由分号或回车隔开将被定义为列向量。
  - `d = [a 6]` 在a的基础上添加新元素6。
  - `[a : step : b]` 创建[a, b]之间的变量，步长为step；注意与python的`range(a, b, step)`区分。
- 向量的构造函数
  - `zeros(M, N)` 创建M行N列的零向量。
  - `ones(M, N)` 创建M行N列的全1向量。
  - `linspace(x1, x2, N)` 创建N个元素的向量，均匀分布于x1和x2。
  - `logspace(x1, x2, N)`  创建N个元素的向量，指数均匀分布于x1和x2。
- 向量元素操作
  - 下标从1开始。
  - `a(3)` 取得第3个元素；注意并非使用中括号。
  - `a(1:2:10)` 取多个元素。
- 向量运算
  - `*` `/` `+` `-` 向量运算
  - 在算符前添加 `.` 对单个元素的运算，如 `a .* 2`
  - 逆转行列 `filplr()`, `flipud()`

## 绘图

绘图前需要设置Graphics Toolkit：

`graphics_toolkit("gnuplot")` 备选："qt"及"gnuplot"

### 绘图指令

- `figure()` 启动一个绘图环境
- `hold on`, `hold off` 保持/不保持上个指令的绘制状态

- 图注 `title('标题')`
- 坐标标签 `xlabel()` `ylabel()`
- 坐标轴 `axis(xbegin, xend, ybegin, yend)`
- 坐标格 `grid on`

### `plot(x, y)`

- `plot(x, y)`
- 自定义标记 `plot(x, y, '+')`
- 修改标记大小 `plot(x, y, '+', 'MarkerSize', 12)`
- 修改线宽 `plot(x, y, 'LineWidth', 5)`

### 输出为图片

`print('figure.png', '-dpng')`;

## 逻辑

```matlab
if expression
    statements
elseif expression
    statements
else
    statements
end

switch x
    case x1
        statements
    otherwise
        statements
end

for varible = vector
    statements
end

while expression
    statements
end
```

## 数据处理

### 求值

1. 平均值 `mean()`
2. 近似整数 `round()`
3. 算术平方根 `sqrt()`

### 拟合

线性拟合工具 `P = polyfit(x, y, n)` n为拟合曲线的次数
线性拟合求值函数 `polyval(P, t)` 返回拟合曲线在t处的值

非线性拟合工具 `lsqcurvefit`

```matlab
% 变温粘滞系数 Figure nw-t 图像 %

nw = [.548, .469, .343, .222, .182];
t = [ 30, 35, 40, 45, 50];

function rslt = fun(var, data)
  rslt = var(1) * exp(-var(2) * data);
endfunction

var0 = [0 0];
P = lsqcurvefit(@fun, var0, t, nw);

plot(t, nw, '+', 'MarkerSize', 12);
plot([25:1:55], fun(P, [25:1:55]), 'LineWidth', 5);
```

---

## 资源

### 教程

- 入门教程 <http://coer.zju.edu.cn/liu/octave-tutorial-cn.pdf>
- 在线网站 <https://octave-online.net/>

## Playground

- [大一下学期的物理实验](https://github.com/lightyears1998/a-gzhu-coder/tree/master/period/freshman/%E7%89%A9%E7%90%86%E5%AE%9E%E9%AA%8C)
