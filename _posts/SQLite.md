---
title: Android Note(2)
description: Note
date: 2016-05-09 15:06:51 +08:00
tags: Note
category: Note
---

### SQLite


不用androidAPI
```
SQLiteDatabase db = oh.getWritableDatabase();  

insert()  
db.execSQL(sql语句, sql语句中的values值);

delete()
db.execSQL(sql语句，sql语句中where查询条件);

update()
db.execSQL(sql语句，sql语句中where查询条件);

select()
db.rawQuery(sql语句,sql语句中where查询条件);
```

使用AndroidAPI
```
insertApi()
db.insert(表名, ,键值数组)

deleteApi()
db.delete(表名, where条件，where条件键值)

updateApi()
db.update(表名，键值数组，where条件，where条件键值)

selectApi()
//第一个表名
//第三个查询字段
//第四个查询where条件
//第六个表示从该条开始查询
//第七个表示查询条数
db.query("person", null, null, null, null, null, null);

```
