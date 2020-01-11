# Powershell

```ps1
# 一行中“#”后的内容被视为注释；
# 命令分隔符为“;”。

# 以管理员身份运行
Start-Process powershell -Verb RunAs "<cmd>" -argumentlist "Arg1", "Arg2"

# 设置代码执行权限
Set-ExecutionPolicy [Unrestricted]

# 获取命令信息
Get-Command [-All] <command>

# 存取环境变量 [ls = Get-ChildItems]
ls env:
$env:Name
$env:name="Value"
```
