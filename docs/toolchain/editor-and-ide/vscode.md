# VS Code

settings.json

```json
"editor.fontFamily": "'Source Code Pro', 'Source Han Serif', Consolas, 'Courier New', monospace"
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

颜色主题：

- Chinolor Theme 使用中国传统配色方案，不太亮又不太暗。

核心拓展：

- VS Live Share
- Visual Studio Intellicode
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
