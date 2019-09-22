# Editor and IDE 编辑器和集成开发环境

## Notepad++

拓展工具：

- HEX-Editor 十六进制编辑
- NppExport 文本带格式导出工具（RTF，HTML）

### 导出为富文本

`插件 > NppExport > Copy RTF to clipboard`

可编辑快捷键`设置 > 管理快捷键...`。

## iteliJ-like IDE

1. 改善字体：更换成Source Code Pro会好一些。

## VS Code

settings.json

```json
"files.insertFinalNewline": true,
"files.autoSave": "onFocusChange",
"files.trimTrailingWhitespace": true,
"files.exclude": {
    "node_modules": true
},
"git.confirmSync": false,
"git.autofetch": true,
"git.enableSmartCommit": true,
```

核心拓展：

- VS Live Share
- Remote Development
- Code Runner

    ```json
    "code-runner.runInTerminal": true,
    "code-runner.executorMap": {
        "java": "cd $dir && javac -encoding utf8 $fileName && java $fileNameWithoutExt",
    }
    ```

- Markdownlint

语言相关：

- C/C++
- Go
- Python

## Visual Studio

### C++

每个版本的VS都有自己的平台工具集，平台工具集包含`MSVCRversion.dll`的调试版本`MSVC...d.dll`。可再发行组件包含平台工具集中的`MSVCRversion.dll`。如果使用了平台工具集相关的DLL，需要确定重新分发的DLL。

- 可以在Property Manager新增属性表（Property Sheet），在新的属性表中定义用户宏（User Marco）。
- C++ 包含目录(`*.h`)、库目录(`*.lib`)和链接器的额外依赖项目(`library.lib`)。

## Arduino相关

- Fritzing 电路图绘制
- Arduino Studio
- Mixly
