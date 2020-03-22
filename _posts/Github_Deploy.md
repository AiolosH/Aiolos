---
title: Hexo Deploy
description: github issue
date: 2020-01-02 10:44:00 +08:00
tags: github issue
category: github issue
---

# hexo d 报错ERROR Deploy not fount:git
报错信息
```
$ hexo d
ERROR Deployer not found: git
```

解决方法
``` 
npm install --save hexo-deployer-git
```