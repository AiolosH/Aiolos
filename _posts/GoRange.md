---
title: Go 键值循环
description: GO
date: 2020-01-05 00:00:00 +08:00
tags: Go
category: Go
---


for range 可以遍历数组、切片、字符串、map 及通道（channel）

数组
``` go
var m = []int{1,2,3,4}
for key, value := range m {
	fmt.Printf("key:%d  value:%d\n", key, value)
}
```

切片
```go
var m = []int{1,2,3,4}
for key, value := range m[1:3] {
	fmt.Printf("key:%d  value:%d\n", key, value)
}
```

字符串
``` go
var str = "hello world"
for key, value := range str {
	fmt.Printf("key:%d value:0x%x\n", key, value)
}
```

map
``` go
m := map[string]int{
    "hello": 100,
    "world": 200,
}
for key, value := range m {
    fmt.Println(key, value)
}
```

channel
``` go
c := make(chan int)
go func() {
	c <- 1
	c <- 2
	c <- 3
	close(c)
}()
for v := range c {
	fmt.Println(v)
}
```