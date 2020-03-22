---
title: DrawText&TextOut效率
description: MFC
date: 2020-01-02 14:30:00 +08:00
tags: MFC
category: MFC
---

# DrawText&TextOut效率

1、内存双缓冲

2、仅可视区域：视图中不可见的区域是不要绘制

3、能用TextOut的地方就别用DrawText，DrawText函数效率极低，会导致CPU占用