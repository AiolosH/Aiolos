---
title: centos 更换源
description: centos 更换源
date: 2016-06-23 13:35:14 +08:00
tags: linux
category: linux
---

#### 修改centos 下载源
备份原来的下载源
```
mv /etc/yum.repos.d/CentOS-Base.repo /etc/yum.repos.d/CentOS-Base.repo.backup
```

转到源目录
```
cd /etc/yum.repos.d/
```

按照自己的版本下载163的源（我是centos7）
```
wget http://mirrors.163.com/.help/CentOS7-Base-163.repo
```

生成缓存
```
yum clean all
yum makecache
```

windows 引导可以进pe修复

centos 修复引导，使用easyBCD，添加一个条目，在linux/BSD选项卡中，type选择grub 2。
