---
title: mysql重置密码
description: 学
date: 2020-02-25 00:00:00 +08:00
tags: 学
category: 学
---

# mysql重置密码

## 1、检查mysql服务是否启动，如果启动，关闭mysql服务

> ps -ef | grep -i mysql

## 2、修改mysql的配置文件my.conf

> vi /etc/my.cnf

``` conf
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock

skip-grant-tables       # 新增语句
```

## 3、重启数据库

> service mysqld start

## 4、进入数据库修改密码

> mysql -u root 

> use mysql;

> update mysql.user set authentication_string=password('root_password') where user='root';  

## 5、删除第二步中增加语句

