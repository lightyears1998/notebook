# Python标准库

## 通用操作系统服务

### [argparse](https://docs.python.org/3/library/argparse.html) 命令行参数、参数和子命令解析
  
## 文件与目录访问

### [pathlib](https://docs.python.org/3/library/pathlib.html)

`os`和`os.path`模块的面向对象封装。

- 构造 `Path(path = '.')`

    ```python
    from pathlib import Path

    Path.home()
    Path.home("Documents")
    ```

- 路径操作
  - `Path.joinpath(str)`
  - `Path.resolve()` 转化为绝对路径
  - `Path.home('.')` 用户目录
  - `Path.cwd()`
  - `Path.exists()`
- 通用操作
  - `Path.stat()`
- 文件操作
  - `Path.is_file()`
  - `Path.touch()`
  - `Path.unlink()`
  - `Path.open()`
  - `Path.read_text(encoding=None)` `Path.write_text()`
  - `Path.read_bytes()`, `Path.write_bytes()`
  - `Path.name`, `Path.suffix`, `Path.suffixs: list`
- 文件夹操作
  - `Path.is_dir()`
  - `Path.rmdir()` 文件夹必须为空
  - `Path.iterdir() -> list`
