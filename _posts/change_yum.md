---
title: CENTOS7 更换源
description: CENTOS
date: 2016-11-14 14:05:14 +08:00
tags: CENTOS
category: CENTOS
---

### 把 yum源 CENTOS 更换成网易 yum源

1、备份你的原镜像文件，以免出错后可以恢复。
```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```
2、下载新的CentOS-Base.repo 到/etc/yum.repos.d/
CentOS 5
```
cd /etc/yum.repos.d/
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
```

3、运行yum makecache生成缓存
```
yum clean all
yum makecache
```
