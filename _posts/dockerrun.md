---
title: docker 问题记录
description: 问题记录
date: 2020-02-25 00:00:00 +08:00
tags: 问题记录
category: 问题记录
---

# docker 问题记录
## 问题来源  
centos7.2 yum 安装docker，运行hello-world
> yum -y install docker
> docker run hello-world

发现docker有如下报错
```
Error response from daemon: oci runtime error: container_linux.go:247: starting container process caused "write parent: broken pipe"...
```

1、通过uname -r命令查看你当前的内核版本
> uname -r

2、更新yum 包到最新
> sudo yum update

3、安装过旧版本, 先卸载旧版本
> sudo yum remove docker  docker-common docker-selinux dockesr-engine

4、安装需要的软件包， yum-util 提供yum-config-manager功能，另外两个是devicemapper驱动依赖的
> sudo yum install -y yum-utils device-mapper-persistent-data lvm2

5、设置yum 源
> sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

6、查看所有仓库中所有docker版本(可选)
> yum list docker-ce --showduplicates | sort -r

7、安装docker
>sudo yum install docker-ce

8、启动并加入开机启动
> sudo systemctl start docker
> sudo systemctl enable docker

9、验证安装是否成功
> docker version