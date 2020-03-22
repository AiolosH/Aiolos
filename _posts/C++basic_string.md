---
title: basic_string
description: C++
date: 2020-01-06 00:00:00 +08:00
tags: C++
category: C++
---

## basic_string
字符串类模板

## string获取字符串长度
string 类自身可以管理内存。string 类提供的各种操作函数大致分为八类：构造器和析构器、大小和容量、元素存取、字 符串比较、字符串修改、字符串接合、I/O 操作以及搜索和查找。

String 类型对象包括三种求解字符串长度的函数：size() 和 length()、 maxsize() 和 capacity()：
- size() 和 length()：这两个函数会返回 string 类型对象中的字符个数，且它们的执行效果相同。
- max_size()：max_size() 函数返回 string 类型对象最多包含的字符数。一旦程序使用长度超过 max_size() 的 string 操作，编译器会拋出 length_error 异常。
- capacity()：该函数返回在重新分配内存之前，string 类型对象所能包含的最大字符数。

## string获取字符串元素：[]和at()
- 下标操作符 []
- 成员函数 at()

这两种访问方法是有区别的：
- 下标操作符 [] 在使用时<b>不检查</b>索引的有效性，如果下标超出字符的长度范围，会示导致未定义行为。对于常量字符串，使用下标操作符时，字符串的最后字符（即 '\0'）是有效的。对应 string 类型对象（常量型）最后一个字符的下标是有效的，调用返回字符 '\0'。
- 函数 at() 在使用时会检查下标是否有效。如果给定的下标超出字符的长度范围，系统会抛出 out_of_range 异常。
``` C++
#include <iostream>
#include <string>
int main()
{
    const std::string str("teststring");
	std::string sss("invoker");
	char temp = 0;
	char temp_1 = 0;
	char temp_2 = 0;
	char temp_3 = 0;
	char temp_4 = 0;
	char temp_5 = 0;
	temp = sss[2];					//"获取字符 'v'
	temp_1 = sss.at(2);				//获取字符 'v'
	temp_2 = sss[sss.length()];		//未定义行为，返回字符'\0'，但Visual 2017未报错
	temp_3 = str[str.length()];		//指向字符 '\0'
	temp_4 = sss.at(sss.length());	//程序异常  std::out_of_range
	temp_5 = str.at(str.length());	//程序异常  std::out_of_range
	std::cout << temp << temp_1 << temp_2 << temp_3 << temp_4 << temp_5 << std::endl;
    return 0;
}
```

## string字符串比较

比较的两个字符串，任一个字符串均不能为 NULL，否则程序会异常退出。
### compare()
使用 compare() 函数时，参数中出现了位置和大小，比较时只能用指定的子串
```C++
s.compare {pos,n, s2);
```
<b><u>区分大小写</u></b>，字符串相同返回0，串S 按字典顺序要先于串S2，返回负值；反之，返回正值

### 比较运算符 
大于(>) 、小于(<) 、等于 、大于等于(>=) 、小于等于(<=>) 、不等于(!=)

## string字符串修改和替换

### assign()
可以直接给字符串赋值。既可以将整个字符串赋值给新串，也可以将字符串的子串赋值给新串。
```c++
basic_string& assign (const E*s); //直接使用字符串赋值
basic_string& assign (const E*s, size_type n);
basic_string& assign (const basic_string & str, size_type pos, size_type n);
//将str的子串赋值给调用串
basic_string& assign (const basic_string& str);    //使用字符串的“引用”賦值
basic_string& assign (size_type n, E c) ; //使用 n个重复字符賦值
basic_string& assign (const_iterator first, const_iterator last);    //使用迭代器赋值
```
### operate=
赋值
### erase()
```C++
terator erase (iterator first, iterator last);
iterator erase (iterator it);
basic_string& erase (size_type p0 = 0, size_type n = npos);
```

示例
```C++
string str1("teststring");
str1.erase(5);  //  str="tests"
str2.erase(str2.begin(), str2.end()); // str=""
```

### swap()
交换

```C++
void swap (basic_string& str);
```

示例
```C++
string str1("teststring");
string str2;
str2.swap(str1);        // str2="teststring" str1=""
```
### insert()
插入字符串

```C++
basic_string& insert (size_type p0 , const E * s); //插人 1 个字符至字符串 s 前面
basic_string& insert (size_type p0 , const E * s, size_type n); // 将 s 的前 3 个字符插入p0 位置
basic_string& insert (size_type p0, const basic_string& str);
basic_string& insert (size_type p0, const basic_string& str,size_type pos, size_type n); //选取 str 的子串
basic_string& insert (size_type p0, size_type n, E c); //在下标 p0 位置插入  n 个字符 c
iterator insert (iterator it, E c); //在 it 位置插入字符 c
void insert (iterator it, const_iterator first, const_iterator last); //在字符串前插入字符
void insert (iterator it, size_type n, E c) ; //在 it 位置重复插入 n 个字符 c
```

```C++
string str1("ello");
string str2("h") ;
str2.insert(1,str1); // str2="hello"
```

### append()
追加字符串
```C++
basic_string& append (const E * s); //在原始字符串后面追加字符串s
basic_string& append (const E * s, size_type n);//在原始字符串后面追加字符串 s 的前 n 个字符
basic_string& append (const basic_string& str, size_type pos,size_type n);//在原始字符串后面追加字符串 s 的子串 s [ pos,…,pos +n -1]
basic_string& append (const basic_string& str);
basic_string& append (size_type n, E c); //追加 n 个重复字符
basic_string& append (const_iterator first, const_iterator last); //使用迭代器追加
```

```C++
string str1("ello");
string str2("h") ;
str2.append(str1); // str2="hello"
```

### replace()
字符串替换

```C++
basic_string& replace (size_type p0, size_type n0, const E * s); //使用字符串 s 中的 n 个字符，从源串的位置 P0 处开始替换
basic_string& replace (size_type p0, size_type n0, const E *s, size_type n); //使用字符串 s 中的 n 个字符，从源串的位置 P0 处开始替换 1 个字符
basic_string& replace (size_type p0, size_type n0, const basic_string& str); //使用字符串 s 中的 n 个字符，从源串的位置 P0 处开始替换
basic_string& replace (size_type p0, size_type n0, const basic_string& str, size_type pos, size_type n); //使用串 str 的子串 str [pos, pos + n-1] 替换源串中的内容，从位置 p0 处开始替换，替换字符 n0 个
basic_string& replace (size_type p0, size_type n0, size_type n, E c); //使用 n 个字符 'c' 替换源串中位置 p0 处开始的 n0 个字符
basic_string& replace (iterator first0, iterator last0, const E * s);//使用迭代器替换，和 1) 用法类似
basic_string& replace (iterator first0, iterator last0, const E * s, size_type n);//和 2) 类似
basic_string& replace (iterator first0, iterator last0, const basic_string& str); //和 3) 类似
basic_string& replace (iterator first0, iterator last0, size_type n, E c); //和 5) 类似
basic_string& replace (iterator first0, iterator last0, const_iterator first, const_iterator last); //使用迭代器替换
```

## string字符串输入输出

- 输入输出流\>> << 
- getline()

## string字符串查找
### find()和 rfind()

### find_first_of()函数和 find_last_of()函数

- find_first_of() 函数可实现在源串中搜索某字符串的功能，该函数的返回值是被搜索字符串的第 1 个字符第 1 次出现的下标（位置）。若查找失败，则返回 npos。

- find_last_of() 函数同样可实现在源串中搜索某字符串的功能。与 find_first_of() 函数所不同的是，该函数的返回值是被搜索字符串的最后 1 个字符的下标（位置）。若查找失败，则返回 npos。

### find_first_not_of()函数和 find_last_not_of()函数

- find_first_not_of() 函数可实现在源字符串中搜索与指定字符（串）不相等的第 1 个字符；
- find_last_not_of() 函数可实现在源字符串中搜索与指定字符（串）不相等的最后 1 个字符。

## string迭代器、配置器