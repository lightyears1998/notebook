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

# 初始化/移除虚拟环境
export PIPENV_VENV_IN_PROJECT=1 # 将虚拟环境创建在项目中
pipenv --two        # 使用Python2初始化虚拟环境
pipenv --three      # 使用Python3
pipenv --python 3.6 # 使用Python3.6
pipenv --rm         # 移除创建的虚拟环境

pipenv --where
pipenv --venv        # 显示虚拟环境信息
pipenv --py          # 显示Python解释器信息

# 包管理
pipenv install <package-name>
pipenv install
pipenv sync
```

Pipfile

```conf
[[source]]
name = "tuna"
url = "https://pypi.tuna.tsinghua.edu.cn/simple"
verify_ssl = true

[dev-packages]
pylint = "*"

[packages]
requests = {extras = ["socks"],version = "*"}
pyyaml = "*"
fire = "*"

[requires]
python_version = "3"

[scripts]
pylint = "pylint ./__main__.py ./packagedir"
```

## Virtualenv

- 在指定目录创建虚拟环境 `virtualenv "venv"`，`--no-site-packages`参数是默认的。
