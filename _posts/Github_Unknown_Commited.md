---
title: Github Unknown Commited
description: github issue
date: 2016-05-13 15:22:51 +08:00
tags: github issue
category: github issue
---

### Github Unknown Commited 问题

问题如图，是通过同一个用户进行提交

![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/commited.png)

看到以前提交的commit都是有用户提交的，在我换了ssd和重装系统之后，重新将项目通过git bash 提交代码，就出现了Unknown Commited，这时发现我的Contribution 就不会增加，最近看着实在难受，就折腾了一下发现，我的git bash 提交不需要输入邮箱和密码，看了github的help，就重新设置了   

```
git config --global user.email "your_email@example.com"
```

然后再输入

```
git config --global user.email
```

屏幕上会打印出你的邮箱地址，在此进行提交发现已经用户名已经回来了。


具体github help 点击以下网址。
https://help.github.com/articles/setting-your-email-in-git/
