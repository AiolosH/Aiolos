---
title: CENTOS7 安装erlang
description: CENTOS
date: 2016-11-15 15:05:14 +08:00
tags: CENTOS
category: CENTOS
---


### install erlang

environment : CENTOS7


首先下载 安装包
```
wget http://erlang.org/download/otp_src_R14B04.tar.gz
```
解压安装包
```
tar -zxvf  otp_src_R14B04.tar.gz
```
转到解压的文件夹下
```
cd otp_src_R14B04.tar.gz
```
最好在root下运行，without-javac 不用javac编译
```
./configure --prefix=/home/erlang   --without-javac
```
进行make
```
make && make install
```
最后加一个软连接
```
ln -s /home/erlang/bin/erl /usr/local/bin/erl
```

最后测试一下
```
erl
```
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/installerlang.png)   

Done!!
