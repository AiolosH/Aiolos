---
title: Android Note(1)
description: Note
date: 2016-05-07 14:08:51 +08:00
tags: Note
category: Note
---

### 按钮点击事件

1、使用内部类   
2、使用匿名内部类   
3、实现onclick接口   
4、button 设置属性onclick,并在类中定义一个相同名称的public方法，需要传入一个view对象，view对象是出发方法执行的组建对象，多个对象可以使用通过方法，通过资源id来判断


### 内部存储和外部存储
内部存储 ：getFilesDir();

外部存储 ：Environment.getExternalStorageDirectory();
必须检查外部存储是否存在 ：Environment.getExternalStorageState();

SD卡状态：
```
MEDIA_REMOVED ：SD卡移除（SD卡不存在）   
MEDIA_UNMOUNTED : SD卡未挂载（SD卡存在，但未挂载）   
MEDIA_CHECKING : SD卡正在遍历   
MEDIA_MOUNTED : SD卡可读
```

### 文件访问权限
drwxrwxrwx   
  * 第一个字母
      * d表示文件夹
      * -表示文件
  * 第一组rwx 描述文件拥有者（owner）的权限
      * r读
      * w写
      * x可执行
  * 第二组rwx：与文件拥有者同一用户组的用户（grouper）
  * 第三组rwx：其他用户（other）的权限
