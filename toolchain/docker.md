# Docker笔记

容器。

## 基本概念

1. **镜像** *Image* 通过运行Image来启动Container
2. **容器** *Container* Image的运行时实体

## 常用操作

- `docker info` 显示详细的Docker安装信息
- `docker ps` 显示正在运行的容器；若要显示已经停止的容器，使用`docker ps --all` `-q`或`--quiet`安静模式显示
- `docker run` 运行容器 `-p host-port:container-port` `--name given-name` `-e ENV_VAR=value`
- `docker container ls`是`docker ps`的同义词
- `docker kill` 终止运行中的容器
- `docker container stop`是`docker kill`的同义词
- `docker container rm <Name-of-container>` 移除容器

镜像仓库相关

- `docker search <name>` 搜索镜像
- `docker pull <name>` 拉取镜像

### 测试Docker是否正常安装

- `docker run hello-world`

## DockerFile

`Dockerfile`用于定义容器，通过`docker build`来生成对应dockerfile的镜像

---

## 安装

```sh
yum install docker
systemctl start docker
```

---

## 链接

- [新手入门](https://docs.docker.com/get-started/)
