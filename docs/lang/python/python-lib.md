# Python Library

- 运行模块 `python -m <module>`

## 环境相关库

### Pip

第三方包被安装在Python的`site-packages`目录下。

- [清华大学Pypi镜像](https://mirror.tuna.tsinghua.edu.cn/help/pypi/)

```bash
pip install [--upgrade] <package-name>

```

### Virtualenv

- 在指定位置创建虚拟环境 `virtualenv "venv"` 默认启用`--no-site-packages`参数

### Pipenv

初始化环境

```sh
pipenv --two

pipenv --threee      # 或者
pipenv --python 3.6

pipenv --where
pipenv --venv        # 显示虚拟环境信息
pipenv --py          # 显示Python解释器信息
```

```sh
pipenv install [--dev] <packagename>
pipenv unistall [--all]
pipenv shell
pipenv run <command>
pipenv graph # 依赖图
```

## 网页处理

### 使用urllib中的request

- [Python Docs](https://docs.python.org/3/library/urllib.html)

```py
from urllib import request

url = 'http://www.baidu.com'
with request.urlopen(url) as f:
    print(f.read())

```

## 字符识别 Tesserocr

OCR识别引擎Tesseract的Python接口

### 安装

Windows:

1. 安装Tesseract，并将`path/to/tesseract`添加到`Path`变量，并设置`TESSDATA_PREFIX`环境变量为`path/to/tesseract/tessdata`（否则调用API时将报错“Invalid tessdata path”）。
2. Windows下通过`pip`安装涉及编译过程，较为困难；通过预编译的`.whl`文件安装较为简单。

## 关系运算包Pandas

<https://pandas.pydata.org/>

## 爬虫控制Selenium

<https://morvanzhou.github.io/tutorials/data-manipulation/scraping/5-01-selenium/>
