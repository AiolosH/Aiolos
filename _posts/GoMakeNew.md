---
title: Go make和new关键字
description: GO
date: 2020-01-05 00:00:00 +08:00
tags: Go
category: Go
---

# Go new和make的区别与实现

## new 的实现
``` go
// The new built-in function allocates memory. The first argument is a type,
// not a value, and the value returned is a pointer to a newly
// allocated zero value of that type.
func new(Type) *Type
```

new 函数只接受一个参数，这个参数是一个类型，并且返回一个指向该类型内存地址的指针。分配的内存置为零，也就是类型的零值。

为基础类型分配空间
``` go
func main() {
	var sum *int
	sum = new(int) //分配空间
    fmt.Println(*sum) // 输出0 会默认置零
    
	*sum = 100
	fmt.Println(*sum) // 输出100
}
```

为自定义类型分配空间
``` go
type Student struct {
   name string
   age int
}

var s *Student
s = new(Student) // 分配空间
s.name ="dequan" 
fmt.Println(s)   // 输出&{dequan 0}
```

## make 的实现

``` go
// The make built-in function allocates and initializes an object of type
// slice, map, or chan (only). Like new, the first argument is a type, not a
// value. Unlike new, make's return type is the same as the type of its
// argument, not a pointer to it. The specification of the result depends on
// the type:
// Slice: The size specifies the length. The capacity of the slice is
// equal to its length. A second integer argument may be provided to
// specify a different capacity; it must be no smaller than the
// length, so make([]int, 0, 10) allocates a slice of length 0 and
// capacity 10.
// Map: An empty map is allocated with enough space to hold the
// specified number of elements. The size may be omitted, in which case
// a small starting size is allocated.
// Channel: The channel's buffer is initialized with the specified
// buffer capacity. If zero, or the size is omitted, the channel is
// unbuffered.
func make(t Type, size ...IntegerType) Type
```

make 也是用于内存分配的，但是和 new 不同，它只用于 chan、map 以及 slice 的内存创建，而且它返回的类型就是这三个类型本身，而不是他们的指针类型，因为这三种类型就是引用类型，所以就没有必要返回他们的指针了。


## new 和 make 区别：

区别 | new | make 
- | - | -
可分配的数据类型 | 任意类型 | slice、map、chan
返回值 | 返回指针 *Type | 返回引用 Type
初始化 | 清零 | 分配后初始化
