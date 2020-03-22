---
title: docker 使用
description: docker
date: 2020-02-25 00:00:00 +08:00
tags: docker
category: docker
---

# docker 容器使用

### 查看正在运行的容器
> docker ps

### 查看对应容器ID或容器名称的端口映射 参数容器ID/名
> docker port (container ID / container name)

### 查看容器进程
> docker top 

### 查看容器日志
> docker logs -f (container ID)

-f:让 dokcer logs 像使用 tail -f 一样来输出容器内部的标准输出。

### 删除容器 参数容器名
> docker rm (container ID / container name)

### 查看所有镜像
> docker images

```
REPOSITORY | TAG | IMAGE ID | CREATED | SIZE
```

NAME: 表示镜像的仓库源

TAG: 镜像的标签

IMAGE ID: 镜像ID

CREATED: 镜像创建时间

SIZE: 镜像大小

### 查找镜像
可以从 Docker Hub 网站来搜索镜像，Docker Hub 网址为： https://hub.docker.com/

> docker search jenkins

```
NAME | DESCRIPTION | STARS | OFFICIAL | AUTOMATED
```

NAME: 镜像仓库源的名称

DESCRIPTION: 镜像的描述

OFFICIAL: 是否 docker 官方发布

stars: 类似 Github 里面的 star，表示点赞、喜欢的意思。

AUTOMATED: 自动构建。

### 拉取镜像
> docker pull

### 运行镜像

> docker run

### 创建镜像
当我们从docker镜像仓库中下载的镜像不能满足我们的需求时，我们可以通过以下两种方式对镜像进行更改。

* 1.从已经创建的容器中更新镜像，并且提交这个镜像
- 2.使用 Dockerfile 指令来创建一个新的镜像

### 更新镜像
更新镜像之前，我们需要使用镜像来创建一个容器。