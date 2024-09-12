# Go 语言常识

[![code-sandbox](https://img.shields.io/badge/code--sandbox-29b7cb.svg)](https://github.com/lightyears1998/code-sandbox/blob/master/lang/go)

- <https://golang.org>
- <https://play.golang.org>
- <https://blog.golang.org>

## Module 模式代码组织

阅读以下文档：

- 现代 Go 代码组织 <https://go.dev/doc/code>
- `GOPATH` 的历史 <https://go.dev/wiki/GOPATH>
- Go Module <https://go.dev/blog/using-go-modules>

## `GOPATH` 模式代码组织（废弃）

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

---

## 命令行工具 `go`

### 包管理工具 `go get`

```sh
go get -flags <package>  # 远程包导入
```

- `<package>`可以是url，也可以是`all`。
- `-fix`
- `-u` update
- `-v` verbose

#### 为`go get`设置HTTP代理

`go` 服从 `http_proxy` 和 `https_proxy`。

```bash
http_proxy=127.0.0.1:8080 go get code.google.com/p/go.crypto/bcrypt
```

```cmd
set http_proxy=http://[user]:[pass]@[proxy_ip]:[proxy_port]/
set https_proxy=http://[user]:[pass]@[proxy_ip]:[proxy_port]/
```

---

## 开发工具

```sh
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.io,direct
go install github.com/mdempsky/gocode@latest
go install github.com/uudashr/gopkgs/cmd/gopkgs@latest
go install github.com/ramya-rao-a/go-outline@latest
go install github.com/acroca/go-symbols@latest
go install golang.org/x/tools/cmd/guru@latest
go install golang.org/x/tools/cmd/gorename@latest
go install github.com/go-delve/delve/cmd/dlv@latest
go install github.com/stamblerre/gocode@latest
go install github.com/rogpeppe/godef@latest
go install github.com/sqs/goreturns@latest
go install golang.org/x/lint/golint@latest
```
