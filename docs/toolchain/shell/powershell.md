# Powershell

```ps1
# 一行中“#”后的内容被视为注释；
# 命令分隔符为“;”。
# 与CMD兼容，指令名与环境变量名均不区分大小写。

# 以管理员身份运行
Start-Process powershell -Verb RunAs "<cmd>" -argumentlist "Arg1", "Arg2"

# 设置代码执行权限
Set-ExecutionPolicy [Unrestricted]

# 获取命令信息
Get-Command [-All] <command>

# 存取环境变量 [ls = Get-ChildItems]
ls env:
$env:Name
$env:Name="Value"
echo $env:Name
echo ${env:Name}
echo "The value of 'Name' is '$env:Name'."
```

## 常量

```ps1
$env:HTTP_PROXY = 'http://host:port'
```

---

## 第三方库

- `Invoke-Environment` <https://github.com/majkinetor/posh/blob/master/MM_Admin/Invoke-Environment.ps1>
