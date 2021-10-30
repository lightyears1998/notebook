# TCL 文件

## 基本文件操作

- `puts ?-nonewline? ?fileID? string`
- `read ?-nonewline? fileID`
- `read fileID numBytes`
- `seek fileID offset ?origin?`
- `tell fileID`
- `flush fileID`
- `eof fileID`

### `open`

`open fileName ?access? ?permissions?`

返回一个可用在 `gets` 和 `puts` 的 FileID。

### `close`

`close fileID`

### `gets`

`gets fileID ?varName?`

``` tcl
set infile [open "myfile.txt"]
while { [gets $infile line] >= 0 } {
    ...
}
```

### `puts`

`puts ?-nonewline? ?fileID? string`

## `file` 命令

提供了文件（目录）操作的高级接口。

## `glob` 命令
