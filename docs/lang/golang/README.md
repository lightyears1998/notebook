# Go语言笔记

[![code-sandbox](https://img.shields.io/badge/code--sandbox-29b7cb.svg)](https://github.com/lightyears1998/code-sandbox/blob/master/lang/go)

<https://golang.org>

<https://play.golang.org>

<https://blog.golang.org>

## 运行环境

### 在Linux上安装Go

<https://www.digitalocean.com/community/tutorials/how-to-install-go-1-7-on-centos-7>

## 代码组织

所有的Go代码被组织在一个工作空间`GOPATH`中（由环境变量`GOPATH`指定）。

```txt
GOPATH/
    bin/
    pkg/
    src/
```

- 可直接运行的命令行工具应当放置在`main`包中。

## 基本结构

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, world!")
}
```



## 命令行工具 `go`

### 包管理工具 `go get`

```sh
go get -flags <package>  # 远程包导入
```

- `<package>`可以是url，也可以是`all`。
- `-fix`
- `-u` update
- `-v` verbose

HTTP代理

```bash
http_proxy=127.0.0.1:8080 go get code.google.com/p/go.crypto/bcrypt  
```

```cmd
set http_proxy=http://[user]:[pass]@[proxy_ip]:[proxy_port]/
set https_proxy=http://[user]:[pass]@[proxy_ip]:[proxy_port]/
```

## 开发工具

```sh
go get -u github.com/mdempsky/gocode
go get -u github.com/uudashr/gopkgs/cmd/gopkgs
go get -u github.com/ramya-rao-a/go-outline
go get -u github.com/acroca/go-symbols
go get -u golang.org/x/tools/cmd/guru
go get -u golang.org/x/tools/cmd/gorename
go get -u github.com/go-delve/delve/cmd/dlv
go get -u github.com/stamblerre/gocode
go get -u github.com/rogpeppe/godef
go get -u github.com/sqs/goreturns
go get -u golang.org/x/lint/golint
```

