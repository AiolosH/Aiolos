---
title: Github Upload
description: github issue
date: 2016-12-01 16:43:51 +08:00
tags: github issue
category: github issue
---

#### 把代码提交到github

1、首先需要安装git客户端

2、配置信息
```
git config --global user.name "your name"
git config --global user.email "your email"
```

3、在github上创建一个仓库test

4、在本地创建项目
```
git init
git commit -m
git remote add origin git@github.com:username/test.git
git push -u origin master
```

#### 将代码从github上pull下来
同样需要创建本地项目
```
git init
git remote add origin git@github.com:username/test.git
```

git pull
```
git pull origin master
```
