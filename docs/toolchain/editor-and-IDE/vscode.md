# VS Code

## `settings.json`

```json
"editor.fontFamily": "'Source Code Pro', 'Source Han Serif', Consolas, 'Courier New', monospace"
"files.insertFinalNewline": true,
"files.trimTrailingWhitespace": true,
"files.exclude": {
    "node_modules": true
},
"git.confirmSync": false,
"git.autofetch": true,
"git.enableSmartCommit": true,
```

## 颜色主题

* **Chinolor Theme** 使用中国传统颜色的配色方案。

## 拓展

* **VS Live Share**
* **Visual Studio Intellicode**
* **Remote Development Pack**
* **Code Runner**

    ```json
    "code-runner.runInTerminal": true,
    "code-runner.executorMap": {
        "java": "cd $dir && javac -encoding utf8 $fileName && java $fileNameWithoutExt",
    }
    ```

与特定上下文结合使用的拓展工具：

* **Markdown** Markdownlint
* **C/C++**
* **Go** Go pack
* **Python**
* **Java** Java Development Pack
