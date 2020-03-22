---
title: 软件设计师准备笔记 Note(5)
description: SDNote
date: 2016-05-19 09:03:20 +08:00
tags: SDNote
category: Note
---


#### 排序算法性能

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/suanfaxingneng.png)

#### 文法分类

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/wenfa.png)

#### 各个键码

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/jianma.png)

#### 无损连接


#### UML视图

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/gezhongshitu.png)

#### 基于各个协议的应用
TCP——TELNET   
UDP——TFTP   
IP——OSPF   
IMCP——PING

#### SPOOLing 技术
将独占设备改造成为共享设备，实现虚拟设备功能，提高独占设备的利用率。

#### DVD-ROM 比 CD-ROM 利用率高
降低了读取激光技术，提高了光学物镜数值孔径，所以提升了存储容量
单面DVD-ROM是4.7GB, 双面DVD-ROM17GB。


#### 基本关系代数
并、差、广义笛卡儿积、投影、选择

#### ATM
电路交换和分组交换的结合

#### 常用端口
* BGP在传输层采用TCP来传送路由信息，使用的端口号179   
* ftp协议监听21（控制连接），20（数据连接）

#### 数据库
个数：count
总和：sum
外键：foreign key (外键名) references 表名(外键名)
视图：create view 视图名 (显示列表名)
          AS select查询语句
          with check option(强制视图上执行所有语句都必须符合准则);
索引：create unique index 索引名 on 表名(索引联系名)
