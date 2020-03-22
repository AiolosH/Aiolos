---
title: mongoDB 初始
description: NoSQL
date: 2016-06-24 12:50:14 +08:00
tags: NoSQL
category: NoSQL
---

#### MongoDB原子操作

原子操作，要么成功，要么失败，执行成功完成既定任务，失败则还原执行前的状态。

$set ： 用来指定一个键并更新键值，若键不存在则创建
```
{ $set : { field : value } }
```

$unset ： 删除一个键
```
{ $unset : { field : 1} }
```

$inc ：可以对文档的某个值为数字型（只能为满足要求的数字）的键进行增减的操作
```
{ $inc : { field : value } }
```

$push ：把value追加到field里面去，field一定要是数组类型才行，如果field不存在，会新增一个数组类型加进去
```
{ $push : { field : value } }
```

$pushAll ：同push，可以一次增加多个值到一个数组字段
```
{ $pushAll : { field : value_array } }
```

$pull ：从数组内删除一个等于value的值
```
{ $pull : { field : _value } }
```

$addToSet ：增加一个值到数组内，而且只有当这个值不在数组内才增加


$pop ：删除数组的第一个或最后一个元素
```
{ $pop : { field : 1 } }
```

$rename ：修改字段名称
```
{ $rename : { old_field_name : new_field_name } }
```

$bit ：位操作，integer类型
```
{$bit : { field : {and : 5}}}
```

#### explain() 用于查询分析 hint()强制指定使用的索引
MongoDB采用B树索引

在user数据库中有users
```
>use user
> db.users.ensureIndex({gender:1,user_name:1})
> db.users.find({gender:"M"},{user_name:1,_id:0}).explain()
```
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/explain.png)  

indexOnly：true，表示我们使用了索引。   
cursor：因为这个查询使用了索引，如果没使用索引游标类型是BasicVursor。  
n：表示查询返回的文档数量。   
nscanned/nscannedObjects：表明当前这次查询一共扫描了集合中多少个文档，我们的目的是，让这个数值和返回文档的数量越接近越好。   
millis：当前查询所需时间，单位毫秒。   
indexBounds：当前查询具体使用的索引。   

```
> db.users.find({gender:"M"},{user_name:1,_id:0}).hint({gender:1,user_name:1})   
> db.users.find({gender:"M"},{user_name:1,_id:0}).hint({gender:1,user_name:1}).explain()
```
hint来强迫MongoDB使用一个指定的索引,在某些情况下会提升性能。
