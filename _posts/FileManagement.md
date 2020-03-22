---
title: 文件管理之文件分配管理(外存)
description: 文件管理
date: 2016-03-08 09:32:16 +08:00
tags: File Management
category: File Management
---

## 文件管理之文件分配管理(外存)

连续分配，看到就知道是连续的分配一些磁盘块来存储文件。

它的优点：访问速度快，而且访问比较容易。

它的缺点：由于是要求有连续的磁盘块来存放，所以容易产生碎片，降低外存的空间利用，还需要在存取之前知道文件的长度。


链接分配又分为，隐式链接和显式链接。

隐式链接，在目录项中含有开始的盘块位置和结束的盘块位置，每个中间盘块中都会有指向下一个盘块的指针。

它的缺点：它只适合顺序访问，对随机访问是极其低效的，如果要访问中间的盘块，就必须从头开始一块一块找下去，当某处指针出现问题，就会导致整个链的断开，可靠性也较差

为提高检索速度和减小指针所占用空间：可以将几个盘块组成一个簇（cluster）。可以成倍减小查找指定块的时间，而且可以减小指针所占用空间，但是会增加内部碎片。

![](http://img.blog.csdn.net/20150329031646299?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvUGhhbnRvbV9Bc3Nhc3Npbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

显式链接，把刚才放在各个磁盘块中的指针放到一张表中。

由于查找记录的过程是在内存中进行，所以大大提高了检索速度，也减少了访问磁盘的次数，该表称为文件分配表FAT(File Allocation Table)

![](http://img.blog.csdn.net/20150329032531068?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvUGhhbnRvbV9Bc3Nhc3Npbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)


索引分配也分为单级索引分配、多级索引分配、混合索引分配。

单级索引分配，在一个磁盘块中保存着某个文件保存在那些磁盘块的所有块号（也就相当于地址），可以通过这些块号来顺序的访问到这个文件。

它的优点：支持直接访问，避免了碎片产生和文件长度受限的情况，也方便了对文件的操作

![](http://img.blog.csdn.net/20150329033748120?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvUGhhbnRvbV9Bc3Nhc3Npbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast))


多级索引分配，对于一些大文件，在一级索引不够用的情况下，可以在索引块中再建立一级索引，必要时可以建立更多级的索引分配方式。


混合索引分配：将多种索引方式结合形成的一种分配方式，里面包含直接地址，一次间接地址，多次间接地址。直接地址就相当于直接索引，一次间接地址相当于存放了一张索引表的地址，实质就是一级索引分配，多次间接地址，实质就是多级索引分配。

它集成了上面的一些优点和特色，提高小文件的储存的磁盘利用率，同时也可以用来存放一些中型、大型文件。
