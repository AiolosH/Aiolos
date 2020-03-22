---
title: 记录
description: Node
date: 2016-06-07 15:05:14 +08:00
tags: Node
category: Node
---
URL  是URI 的一个子集
URL 是URI
URI 不一定是URL


URL
querystring.stringify()

querystring.parse()
//转义字符
querystring.escape()
//反转义字符
querystring.unescape()



#### nodejs require


#### node.js EventEmitter事件监听
事件监听
on('方法名'， 回调函数)  

事件触发
emit('方法名'， 回调函数参数)
会返回一个布尔值来判断是否被监听过

移除事件监听
removeListener('方法名'， 回调函数)
removeAllListeners('方法名')
第二个如果不设置方法名，会移除所有监听

获取该方法名的监听数目
listeners('方法名').length

设置监听个数，默认为10个
setMaxListeners(10)
