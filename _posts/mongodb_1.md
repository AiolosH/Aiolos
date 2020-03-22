---
title: mongoDB 初始
description: NoSQL
date: 2016-06-23 11:05:14 +08:00
tags: NoSQL
category: NoSQL
---

### 初始MongoDB
#### 开启服务
```
$ sudo service mongodb start
```
#### 进入mongodb
```
mongodb
```
#### 创建数据库
```
use [database name]   //切换数据库，使用数据库
```

#### 查看数据库
```
db                    //查看当前数据库
show dbs              //查看所有数据库，不显示没有数据的数据库
```

#### 删除数据库
```
use [need drop database name]  //切换到需要删除的数据库中
db.dropDatabase()
```

#### 创建集合
```
db.createCollection("[collection name]")
```

#### 删除集合
```
db.[need drop collection name].drop()
```
#### 插入文档
```
userdoc1 = ({"user_id":1, "name":"huobingli", "state":"active", "email":"huobingli@outlook.com"})
db.[insert collection].insert(userdoc1)
```

#### 更新文档
```
db.[update collection].update({"user_id":1, "name":"huobingli"}, {$set{"state":"nagetive"}})
```
第一个大括号表示查找条件
第二个大括号表示替换内容
默认是对一个文档进行修改，想要对多个文档进行修改需要写成
```
db.[update collection].update({"user_id":1, "name":"huobingli"}, {
  "state":"nagetive" })
```

#### 替换文档
```
db.[save collection].save({"user_id":1,"name":"george"})
```
save 和insert区别，存在主键，insert报错，save可以
没有主键，都相当于增加一条数据

#### 删除文档
```
db.[remove collection].remove({"name":"huobingli"})
```
