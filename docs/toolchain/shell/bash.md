# Bash

终端前的符号表示用户的权限等级：

- `$` normal user
- `#` Root user：`#`比`$`更接近0。

## 指令格式

`command [-options] parameter1 parameter2...`

- 命令区分大小写。
- 跨行输入命令则需要按下 `\ + Enter`。
- 文件末尾；输入结束使用`Ctrl + D`。

## 脚本

```bash
#!/usr/bin/bash
```

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
