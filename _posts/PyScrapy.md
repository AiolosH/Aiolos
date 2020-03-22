---
title: Scrapy
description: python
date: 2020-01-01 00:00:00 +08:00
tags: python
category: python
---

# Scrapy 爬虫
pycharm生成的目录结构
![](https://raw.githubusercontent.com/huobingli/huobingli.github.io/master/img/scrapy.png)

scrapy.cfg: 项目配置文件   
spider/: 项目python模块, 呆会代码将从这里导入   
spider/items.py: 项目items文件   
spider/pipelines.py: 项目管道文件   
spider/settings.py: 项目配置文件   
spider/spiders: 放置spider的目录   


在 settings.py 文件中，有如下设置
``` python
ROBOTSTXT_OBEY = True
```
robots.txt 是遵循 Robot 协议的一个文件，在 Scrapy 启动后，首先会访问网站的 robots.txt 文件，然后决定该网站的爬取范围。有时我们需要将此配置项设置为 False。
