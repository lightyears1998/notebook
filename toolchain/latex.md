# LaTeX笔记

Continue <https://liam.page/2014/09/08/latex-introduction/>

## Chapter 1 概述

Tex

- 源文件后缀名`.tex`
- LaTeX3正在开发中，LaTeX2e是LaTeX2的改进版。

*Tex*系列名词

- Tex 排版引擎，实现断行、分页等功能的程序；同时也是引擎所使用的标记语言的名称
- LaTex 基于Tex的排版系统，将LaTex新定义的命令翻译为Tex命令
- XeTex or XeLatex 支持Unicode字符的引擎

工具

- **发行版** Tex Live ~~CTex套装（陈旧，现阶段技术的发展已经解决了CTex简化中文处理的初衷）~~
- **宏集** CTex宏集，集成诸多中文排版工具的宏包集合
- **排版工具** XeLaTeX

## Chapger 2 一般结构

```latex
\documentclass{article}
% 这里是导言区
\begin{document}
Hello, world~
\end{document}
```

使用CTex宏包以支持中英混排。

```latex
\documentclass[UTF8]{ctexart}
\title{你好，世界}
\author{lightyears1998}
\date{\today}
\begin{document}
\maketitle
这是我的第一篇LaTex。
\end{document}
```

### 文章结构

- 目录 `\tableofcontents`
- `\section{TEXT}`, `\subsection{TEXT}`, `\subsubsection{TEXT}`
- `\paragraph{TEXT}`, `\subparagraph{TEXT}`

---

## 安装

在Windows上使用Tex Live，使用XeLaTex进行编译。