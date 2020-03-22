---
title: 初识Oracle
description: Oracle
date: 2016-03-14 14:08:51 +08:00
tags: Oracle Database
category: Oracle
---

## 初始Oracle Database

### 虚拟机环境
虚拟机版本：VMware 12.0 pro   
操作系统：Microsoft Service 2003 R2   
Oracle数据库版本：Oracle 10g

### 创建数据库

#### 建库工具DBCA

使用Oracle的建库工且DBCA，这是一个图形界面工且，使用起来方便且很容易理解，因为它的界面友好、美观，而且提示也比较齐全。在 Ｗindows系统中，这个工具可以在Oracle程序组中打开（”开始”—“程序”—“ Oracle - OraDb10g_home1”—“ Configuration and Migration Tools”（配置和移植工具）—“ Database Configuration Assistant”)


#### 手动建库
手动建库步骤：  
1）创建必要的相关目录   
2）创建初始化参数文件  
3）设置环境变量 ORACLE_SID   
4）创建实例  
5）启动数据库到NOMOUNT状态  
7）执行建库脚本   
8）执行catalog脚本创建数据字典   
9）执行catproc创建package包   
10）执行pupbld   
11）由初始化参数文件创建spfile文件   
12）执行scott脚本创建scott模式   

完成以上步骤就可以使用数据库了。

实验路径在C盘下，数据库名称为MYNEWDB   
1、创建相关目录  
```
C:\>mkdir D:\oracle\product\10.2.0\admin\MYNEWDB   
C:\>mkdir D:\oracle\product\10.2.0\admin\MYNEWDB\bdump   
C:\>mkdir D:\oracle\product\10.2.0\admin\MYNEWDB\udump   
C:\>mkdir D:\oracle\product\10.2.0\admin\MYNEWDB\cdump    
C:\>mkdir D:\oracle\product\10.2.0\admin\MYNEWDB\pfile   
C:\>mkdir D:\oracle\product\10.2.0\admin\MYNEWDB\create   
C:\>mkdir D:\oracle\product\10.2.0\oradata\MYNEWDB   
```
也可以将系统的已经创建的目录拷贝过去，将里面文件删除即可

各个目录用途：
其中 C:\oracle\product\10.2.0\admin\MYNEWDB 目录下的几个子目录主要用于存放数据库运行过程中的跟踪信息。最重要的两上子目 录是bdump和udump目录，bdump目录存放的是数据库动行过程中的各个后台进程的跟踪信息，当中alert文件是警告文件，其文件名称为 alert_book.log，当数据库出现问题时，首先就可以去查看此文件以找出原因，手工创建过程中出现的各种问题往往也可以通过查看这个文件找到原 因。udump目录存放和特定会话相关的跟踪信息。C:\oracle\product\10.2.0\oradata\MYNEWDB目录存放各种数据库文 件，包括控制文件、数据文件、重做日志文件。

2、创建初始化参数文件

我们在安装Oracle的时候，系统已经为我们安装了一个名为orcl的数据库，于是我们可以从它哪里得到一份初始化参数文件。打开目录 C:\oracle\product\10.2.0\admin\orcl\pfile，找到init.ora文件，把它拷贝到 C:\oracle\product\10.2.0\bd_1\databse下，并将其改名为 initMYNEWDB.ora。接着用记事本的方式打开initMYNEWDB.ora。
修改以下的内容：
```
db_domain=""   
db_name=book   
control_files=("C:\oracle\product\10.2.0\oradata\MYNEWDB\control01.ctl", "C:\oracle\product\10.2.0\oradata\MYNEWDB\control02.ctl", "C:\oracle\product\10.2.0\oradata\MYNEWDB\control03.ctl")    
undo_management=AUTO   
undo_tablespace=UNDOTBS1　――注意此处的“UNDOTBS1”要和建库脚步本中对应  
background_dump_dest=C:\oracle\product\10.2.0\admin\MYNEWDB\bdump   
core_dump_dest=C:\oracle\product\10.2.0\admin\MYNEWDB\cdump   
user_dump_dest=C:\oracle\product\10.2.0\admin\MYNEWDB\udump
```
3、设置环境变量ORACLE_SID
```
C:\>SET ORACLE_SID = MYNEWDB
```

4、创建实例（服务）
```
C:\>oradim -new -sid MYNEWDB     //创建一个MYNEWDB的服务  
C:\>oradim -delete -sid XXXX     //删除一个XXXX的服务
```
可以通过在cmd中输入services.msc查询到改服务

5、创建口令文件
```
C:\>orapwd file=C:\oracle\product\10.2.0\db_1\database\pwdMYNEWDB.ora password=MynewDB123 entries=5
```
orapwd是创建口令文件的命令，file参数指定口令文件所在的目录和文件名称，password参数指定sys用户的口令，entries参数指定数据库拥用DBA权限的用户的个数。  

口令文件是专门存放sys用户的口令，因为sys用户要负责建库、启动数据库、关闭数据库等特殊任务，把以sys用户的中令单独存放于口令文件中，这样数据库末打开时也能进行口令验证。

6、启动数据库到NOMOUNT（实例）状态
```
C:\>sqlplus /nolog   
```
SQL>connect sys/MynewDB123 as SYSDBA ---这里是用sys连接数据库   
已连接到空闲例程
```
SQL>startup nomount    
ORACLE 例程已经启动

SQL>
```
