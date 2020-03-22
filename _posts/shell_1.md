---
title: shell program
description: shell program
date: 2016-08-15 14:08:51 +08:00
tags: shell program
category: shell program
---

### shell 编程
shell脚本需要调用其它语言需要加入
```
#!/bin/bash
```
开头加上这句话


#### echo 输出
```
\a 警告音
\b 退格键
\n 换行
\r 回车键
\t 制表符 TAB键
\v 垂直制表符
\0nnn 按照八进制ASCII码表输出字符，其中0为数字零，nnn为三位八进制数
\xhh  按照十六进制ASCII码表输出字符，其中hh是两位十六进制数
```
echo -n 不换行输出   
echo -e 处理特殊字符   

echo开启颜色显示  
```
#30m = 黑色， #31m = 红色， #32m = 绿色， #33m = 黄色
#34m = 蓝色， #35m = 洋红， #36m = 青色， #37m = 白色

格式：开头\e[1;(颜色代码m)    结尾\e[0m  
举个例子： echo "\e[1;31m  hello echo \e[0m"
```

#### 脚本执行
1、可以通过赋予执行权限，直接运行
```
 chmod 755 脚本名.sh
./脚本名.sh
```

2、通过bash执行脚本
```
bash 脚本名.sh
```
