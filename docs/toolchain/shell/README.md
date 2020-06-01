# Shell笔记

- 操作系统和Shell指令索引 <http://ss64.com/>
- Bash Tutorial <https://wangdoc.com/bash/>

## 通用 Shell 工具

``` sh
# 词频统计
cat words.txt | tr --squeeze-repeats ' ' '\n' | sort | uniq --count | sort --reverse | awk '{print $2" "$1}'

# 打印第 10 行
cat file.txt | tail --lines=+10 | head --lines=1
```
