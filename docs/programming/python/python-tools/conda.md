# Conda

Anaconda 或 Miniconda 几乎是必不可少的包管理器。

我对 conda 印象最初停留在 Python 的包管理器，但似乎该刻板印象需要更新。时至今日，<anaconda.org> 上已经积累了不计其数的科研工具包。

## Compilers Toolchain

Conda 甚至附带有 C/C++ 编译器包。这点在我们没有环境中的 root 用户权限时，使用 conda 安装包极为方便。

```
conda create --name cpptool

export CONDA_BUILD=1 # 在 `conda activate` 时，将设置 `$CC` `$ID` 等编译器相关的环境变量。
conda activat
```

注意不要错误地安装了名称相似的 `gcc` 包。`gcc` 包似乎并无作用。
