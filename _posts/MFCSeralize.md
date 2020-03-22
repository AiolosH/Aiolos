---
title: MFC 序列化Serialize
description: MFC
date: 2019-12-01 00:00:00 +08:00
tags: MFC
category: MFC
---

# 永久保存机制(Persistence) 序列化

MFC有一套Serialize机制，目的是把文件名的选择、文件的开关、缓冲区的建立、数据的读写、提取运算符(>>)和插入运算符(<<)的重载、对象的动态创建等都包装起来。


##  Serialize(数据读写)
CArchive 对象提供了一个类型安全缓冲机制, 支持存储数据（即写入数据或将数据序列化）和加载数据（即读取数据或将数据反序列化）

类可以进行文件的读写操作，前提是拥有动态创建能力，设计了一下两个宏

```C++
#define DECLARE_SERIAL(class_name) \
    DECLARE_DYNCREATE(class_name)\
    friend CArchive& AFXAPI operator>>(CArchive& ar, class_name* &pOb);
```

```C++
#define IMPLEMENT_SERIAL(class_name, base_class_name, wSchema) \
    CObject* PASCAL class_name::CreateObject() \
        { return new class_name; } \
    _IMPLEMENT_RUNTIMECLASS(class_name, base_class_name, wSchema, \
        class_name::CreateObject) \
    CArchive& AfxApi operator>>(CArchive& ar, class_name* &pOb) \
        { pOb = (class_name*) ar.ReadObject(RUNTIME_CLASS(class_name)); \
            return ar; }
```