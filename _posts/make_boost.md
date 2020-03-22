---
title: CENTOS7 安装编译Boost库
description: CENTOS
date: 2016-11-15 15:05:14 +08:00
tags: CENTOS
category: CENTOS
---

### linux 下编译Boost库

1、下载Boost库

2、解压压缩文件

3、./bootstrap.sh; ./b2
./bootstrap.sh 是编译前的配置工作
./b2 开始编译

4、/b2 --buildtype=complete stage
将对Boost库进行完整编译，生成所有调试版、发行版的静态库和动态库
buildtype选项是编译类型，如不指定就是release模式
stage选项指定Boost使用本地构建。如果使用install选项则编译后会把Boost安装到默认路径下（/usr/local）


5、首先把Boost库的头文件存放到/usr/include/boost/路径下，再把Lib文件存放到/usr/local/lib/boost/路径下。


6、修改/etc/profile文件，在此文件中增加如下2个环境变量：

BOOST_INCLUDE=/usr/include/boost
export BOOST_INCLUDE

BOOST_LIB=/usr/local/lib/boost
export BOOST_LIB

Done!!!
