---
title: Nginx
description: nginx
date: 2016-06-24 12:50:14 +08:00
tags: nginx
category: nginx
---

## 安装nginx    
1、安装编译工具及库文件
> yum -y install make zlib zlib-devel gcc-c++ libtool  openssl openssl-devel

2、安装 PCRE
作用是让 Nginx 支持 Rewrite 功能。
> cd /usr/local/src/  
> wget http://downloads.sourceforge.net/project/pcre/pcre/8.35/pcre-8.35.tar.gz  
> tar -zxvf pcre-8.35.tar.gz   
> cd pcre-8.35   
> ./configure  
> make && make install  

验证是否安装成功
> pcre-config --version

3、安装nginx
> wget http://nginx.org/download/nginx-1.6.2.tar.gz   
> tar zxvf nginx-1.6.2.tar.gz   
> ./configure --prefix=/usr/local/webserver/nginx --with-http_stub_status_module --with-http_ssl_module --with-pcre=/usr/local/src/pcre-8.35
> make
> make install

验证是否安装成功
> /usr/local/webserver/nginx/sbin/nginx -v

## 常用命令

启动nginx
> ./nginx 

验证配置文件
> ./nginx -t

nginx关闭
> ./nginx -s stop

重新载入nginx配置文件
> ./nginx -s reload


## make 错误时
```
make: *** No rule to make target `build", needed by `default".  Stop.
./configure: error: SSL modules require the OpenSSL library.
You can either do not enable the modules, or install the OpenSSL library
into the system, or build the OpenSSL library statically from the source
with nginx by using --with-openssl=option.
```

解决方案
> yum -y install openssl openssl-devel