# CMD

模拟文件结束：`Ctrl + Z`

```batch
REM 行首的“REM”或“::”标志本行为注释。
:: 注意Batch中空格的使用相当严格。

REM 重定向
command< 输入流 > 输出流
:: 往现有文件末尾追加数据。
command>> 输出流
:: 管道：将前一个命令的输入作为后一个命令的输出。
command_1| command_2

REM 环境变量
:: “=”号两侧不能有空格，否则连同此空格会被作为变量/值的内容。
set SOMETHING=value
set PATH=value;%PATH%
echo %SOMETHING%

REM 定位程序路径
where <command>
```
