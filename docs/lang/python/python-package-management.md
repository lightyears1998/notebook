# Python虚拟环境和包管理

- 使用[清华大学Pypi镜像](https://mirror.tuna.tsinghua.edu.cn/help/pypi/)。
- 使用`pipenv`

## `pip`

```sh
pip install [--upgrade] <package-name>
```

## `pienv`

```sh
pip install pipenv

# 初始化虚拟环境
pipenv --two        # 使用Python2初始化虚拟环境
pipenv --three      # 使用Python3
pipenv --python 3.6 # 使用Python3.6

pipenv --where
pipenv --venv        # 显示虚拟环境信息
pipenv --py          # 显示Python解释器信息

# 包管理
pipenv install <package-name>
pipenv install
pipenv sync
```

## Virtualenv

- 在指定目录创建虚拟环境 `virtualenv "venv"`，`--no-site-packages`参数是默认的。
