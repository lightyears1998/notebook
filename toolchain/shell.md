# Shell笔记

## Bash

- `which`, `whereis`
- 文件结束 `Ctrl + D`

### Bash脚本

- 定义变量：`variable=value`，赋值号两边不能存在空格。

    字符串类型变量

    ```sh
    VARNAME='StringValue'
    ```

    将命令执行的输出赋值给变量：

    ```sh
    RX_BYTES=`cat /sys/devices/virtual/net/br-lan/statistics/rx_bytes`
    ```

- 使用变量 `$VARNAME`
- 执行带变量的命令

    ```sh
    curl -s -o /dev/null "http://509.qfstudio.net/?rx=$RX_BYTES&tx=$TX_BYTES&key=$KEY"
    ```

- 条件

    `-z STRING` 判断STRING是否为空

    ```sh
    minieap_process=`pgrep minieap`
    if [ -z "$minieap_process" ]; then
            # Start MiniEAP when there is none
            if [ "x$1" == "x" ]; then
                    /usr/bin/minieap.sh
                    echo MiniEAP restarted.
            elif [ "x$1" == "xnoexec" ]; then
                    echo MiniEAP is down.
            else
                    echo USAGE: $0 \[noexec\]
                    echo If noexec is given, MiniEAP won\'t be restarted.
            fi
    else
            echo MiniEAP is running.
    fi
    ```

    ```sh
    if [ ! -z "`pgrep minieap`" ]
    then
        /usr/bin/curl https://www.baidu.com > /dev/null
        if [ $? -gt 0 ]
        then
            /usr/bin/restart_minieap.sh
            echo MiniEAP restarted.
        else
            echo MiniEAP works fine.
        fi
    else
        echo MiniEAP is not running.
    fi
    ```

## CMD

- 文件结束 `Ctrl + Z`
- 重定向
  - `命令 < 输入流 > 输出流`
  - `命令 >> 输出流` 往现有文件末尾追加数据。
  - `前一个命令 | 后一个命令` 将前一个命令的输出作为后一个命令的输入。

## Powershell

- 以管理员身份运行 `Start-Process powershell -Verb RunAs "<cmd>" -argumentlist "Arg1", "Arg2"`

- 设置代码执行权限 `Set-ExecutionPolicy [Unrestricted]`
- 存取环境变量 `ls env:`, `$env:Name`, `$env:name="Value"`
