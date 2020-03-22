---
title: 不能连接到mysql.sock  linux下安装MySQL
description: linux
date: 2016-12-05 12:22:51 +08:00
tags: linux
category: linux
---
### ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/lib/mysql/mysql.sock' (2)


#### ubuntu 下安装MySQL
```
sudo apt-get install mysql-server

apt-get isntall mysql-client

sudo apt-get install libmysqlclient-dev
```

#### CentOS7下安装MySQL
因为CentOS7已经默认集成了mariadb,其实mariadb是mysql的一个分支， [大传送门](http://baike.baidu.com/item/mariaDB)   

因为MySQL已经被甲骨文收购，MySQL的所有权也落到Oracle手中，MariaDB现在主要有开源社区维护

之前在启动MySQL时报错

ERROR 2002 (HY000): Can't connect to local MySQL server through socket '/var/lib/

安装MySQL需要将MariaDB的所有东西删除干净

1、查看MariaDB是否被安装
```
rpm -qa | grep mariadb
rpm -e mariadb
```
2、卸载MariaDB的各种包
```
yum remove -y mariaDB(代表包名)
```
3、获取MySQL yum源
```
wget http://dev.mysql.com/get/mysql57-community-release-el7-9.noarch.rpm
```
4、安装MySQL
```
sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
sudo yum install mysql-server
```
5、启动MySQL服务,并设置开机启动
```
systemctl start mysql
systemctl enable mysql
```
6、进入MySQL
```
mysql -u root -p（刚进去是没有密码的直接回车）
update user set password=PASSWORD（’passwd’） where User=’root’;
flush privileges;(刷新权限)
```

简单MySQL使用
(分号！分号！分号！)
```
show databases;
show tables;
select * from (table);
insert into (table) (数据表列表) values (插入数据表值)
update ...
delete ...
```

[小传送门](http://blog.csdn.net/qq_26446443/article/details/53491926)
