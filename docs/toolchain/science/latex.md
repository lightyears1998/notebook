# LaTeX笔记

## 一般结构

```latex
\documentclass{article}
% 这里是导言区

\begin{document}
% 正文区域
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

## 文章结构

- 目录 `\tableofcontents`
- 小节 `\section{TEXT}`, `\subsection{TEXT}`, `\subsubsection{TEXT}`
- 带标题的段落 `\paragraph{TEXT}`, `\subparagraph{TEXT}`

## 多行标题

```latex
\title{
  第一行标题 \\
  第二行标题 \\
  \large 小标题
}
```

## 多位作者

```latex
\author{
  作者A \and 作者B
}
```

## 超链接

```latex
\usepackage{hyperref}

\url{uri://example}
```

## 插入图像

```latex
\usepackage{graphicx}

\begin{figure}[htbp]
  \centering
  \includegraphics[width=\linewidth]{图像的路径}
  \caption{题注}
\end{figure}
```

## 绘制矢量图形

考虑[pgf-tikz](https://github.com/pgf-tikz/pgf)

## 有序列表

```latex
\begin{enumerate}
  \item 列表项3
  \item 列表项3
  \item 列表项3
\end{enumerate}
```

---

## 安装

Tex Live是跨平台的Tex发行包。

使用TeXWorks Editor进行编辑，一般使用XeLatex进行编译。

## 中文支持

全中文的文档应当使用CTex的文档类`ctexart`等，
需要在英文的文档类中使用中文支持的情况下可以使用`\usepackage{ctex}`。

`xeCJK`是为Tex添加中文支持的轮子，日常一般使用高层的`ctex`宏包。

## 参考链接

- LaTeX简介 <https://liam.page/2014/09/08/latex-introduction/>
- Overleaf Latex 教程 <https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes>
- CTex 宏包手册 <http://mirrors.ibiblio.org/CTAN/language/chinese/ctex/ctex.pdf>

---

## Tex发行版：TexLive

### 1. 处理发行版问题

[在旧发行版上安装旧版软件包](https://tex.stackexchange.com/questions/25089/how-to-install-a-package-from-an-older-version-of-texlive)：

```sh
# 存在风险，操作前需要备份。
tlmgr option repository ftp://tug.org/historic/systems/texlive/2010/tlnet-final
```
