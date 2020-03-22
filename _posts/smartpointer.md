---
title: 智能指针
description: C++
date: 2020-01-06 00:00:00 +08:00
tags: C++
category: C++
---

# 智能指针

## 为什么要用智能指针
智能指针的作用是管理指针，为了防止内存泄漏的发生。使用智能指针可以很大程度上的避免这个问题，智能指针是一个类，当超出了其作用域，会<u><b>自动调用</u></b>析构函数，析构函数释放资源，不需要手动释放空间，防止了内存泄漏。需要包含头文件 \<memory\>，主要用于管理动态内存分配。

## auto_ptr

采用所有权模式.
``` c++
auto_ptr<string> p1(new string("test auto_ptr."));
auto_ptr<string> p2;
p2 = p1; //auto_ptr不会报错.  #1

cout << p2->c_str() << endl; // 正常输出
cout << p1->c_str() << endl; // 运行时报错 
```
#1步之后，可以看p1、p2, 发现p1已经为NULL, 原来的p1已经转移到了p2
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/auto_ptr.png)

查看错误信息，报错信息如下 
``` c++
_STL_VERIFY(_Myptr, "auto_ptr not dereferencable"); // auto_ptr不可解引用
```
所以，p1所有权转移到p2的, <font color=#FF2222>运行时访问p1时会报错 </font>

##  unique_ptr  
unique_ptr 用于替换auto_ptr.  
独占式拥有: 保证同一时间内只有一个智能指针可以指向该对象
``` c++
unique_ptr<string> p3(new string("test unique_ptr"));
unique_ptr<string> p4;
p4 = p3;  // 编译时报错
```
避免出现 auto_ptr 的情况

* std::move函数可以将左值引用转换为右值引用
``` c++
unique_ptr<string> p3(new string("test unique_ptr"));
unique_ptr<string> p4;
p4 = std::move(p3); // 这里可以正常赋值

cout << p4->c_str() << endl; // 正常输出
cout << p3->c_str() << endl; // 运行时报错 
```
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/unique_ptr.png)

虽然运行时还是会报错, 但相比auto_ptr 在编译时就直接会报错。

## shared_ptr

shared_ptr实现共享式拥有概念。多个智能指针可以指向相同对象，该对象和其相关资源会在"最后一个引用被销毁"时候释放。  
从名字share就可以看出了资源可以被多个指针共享，它使用计数机制来表明资源被几个指针共享。  
``` c++
shared_ptr<string> p1 = shared_ptr<string>(new string("test shared_ptr."));
    cout << p1.use_count() << endl; // 输出 1
    cout << p1.unique() << endl; // 唯一，输出1

	{
		shared_ptr<string> p2(p1);

        cout << p1.use_count() << endl; // 输出 2
		cout << p2.use_count() << endl; // 输出 2

        cout << p1.unique() << endl; // 不唯一，输出0
	} // 离开 p2 作用域

	cout << p1.use_count() << endl; // 输出 1
    cout << p1.unique() << endl; // 唯一，输出1
```

- use_count()  
来查看引用个数。

- unique()  
返回是否是独占所有权( use_count 为 1)

- swap()  
交换两个 shared_ptr 对象(即交换所拥有的对象)

- reset()  
放弃内部对象的所有权或拥有对象的变更, 会引起原有对象的引用计数的减少

- get()  
返回内部对象(指针), 由于已经重载了()方法, 因此和直接使用对象是一样的.如 shared_ptr<int> sp(new int(1)); sp 与 sp.get()是等价的

## weak_ptr

weak_ptr 是一种不控制对象生命周期的智能指针, 它指向一个 shared_ptr 管理的对象。 它只可以从一个 shared_ptr 或另一个 weak_ptr 对象构造, 它的构造和析构不会引起引用记数的增加或减少。

weak_ptr是用来解决shared_ptr相互引用时的死锁问题,如果说两个shared_ptr相互引用,那么这两个指针的引用计数永远不可能下降为0,资源永远不会释放。

它是对对象的一种弱引用，不会增加对象的引用计数，和shared_ptr之间可以相互转化，shared_ptr可以直接赋值给它，它可以通过调用lock函数来获得shared_ptr。
