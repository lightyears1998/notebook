# Python Library

- 运行模块 `python -m <module>`

## 环境

### Pip

第三方包被安装在Python的`site-packages`目录下。

- [清华大学Pypi镜像](https://mirror.tuna.tsinghua.edu.cn/help/pypi/)

```bash
pip install [--upgrade] <package-name>

```

### Virtualenv

- 在指定位置创建虚拟环境 `virtualenv "venv"` 默认启用`--no-site-packages`参数

## 网页处理

### 使用urllib中的request

- [Python Docs](https://docs.python.org/3/library/urllib.html)

```py
from urllib import request

url = 'http://www.baidu.com'
with request.urlopen(url) as f:
    print(f.read())

```

## tesserocr

OCR识别引擎Tesseract的Python接口

### 安装

Windows:

1. 安装Tesseract，并将`path/to/tesseract`添加到`Path`变量，并设置`TESSDATA_PREFIX`环境变量为`path/to/tesseract/tessdata`（否则调用API时将报错“Invalid tessdata path”）。
2. Windows下通过`pip`安装涉及编译过程，较为困难；通过预编译的`.whl`文件安装较为简单。
