# Python常识

```sh
# The Zen of Python, by Tim Peters
python -c "import this"
```

- 不要使用 Windows 应用商店的 Python 版本。（该版本的 Python 存在[一些限制](https://docs.python.org/3/using/windows.html#known-issues)。）

## 代码组织

```txt
SoftwareName/
   LICENSE.txt
   README.txt
   setup.py
   software_name/
      __init__.py
      script.py
      another_script.py
```

- `__init__.py`通常定义`__version__`字符串。

## 包、包管理工具和虚拟环境

- 使用[清华大学Pypi镜像](https://mirror.tuna.tsinghua.edu.cn/help/pypi/)。`https://pypi.tuna.tsinghua.edu.cn/simple`
- 使用 [`poetry`](https://github.com/python-poetry/poetry) 作为主力的包管理工具。
- `pip`、`virtualenv`、`poetry` 和 `pipenv` 另见于[包管理工具笔记](python-tools/package-management.md)。
