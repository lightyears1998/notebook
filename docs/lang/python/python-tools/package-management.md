# Python 中的包管理

## `pip`

Pip跟随`$HTTP_PROXY`环境变量。

```sh
pip install [--upgrade] <package-name>
```

## `poetry`

``` sh
pip install poetry # 或使用独立的 get-poetry.py 安装方式，详见 poetry 官网。
```

## `pipenv`

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
pipenv install <package-name> [--pypi-mirror <mirror_url>]
pipenv install
pipenv sync
```

注：`pipenv`的[Mutiple sources](https://github.com/pypa/pipenv/issues/716)意图并不是实现Mirror功能；Mirror可使用`--pypi-mirror <mirror_url>`参数。

### Pipfile

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
