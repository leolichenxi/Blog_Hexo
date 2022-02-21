---
title: Lua 内存 和 GC
categories: lua
tags: lua
date: 2021-06-14 12:00:00
toc: true
---
##
1 byte (B 字节) = 8 bits (b 比特位，0或1)
1 KB = 1024 (2^10) byte
1MB = 1024 KB
1GB = 1024 MB
1TB = 1024 GB
##

## 基础数据类型

1. number 实数，可以是整数，浮点数
2. string 字符串，一旦赋值不能被修改，可以通过方法string.gsub()来修改
3. nil 全局变量没被赋值默认为nil，删除变量酒赋值为nil
4. boolean false 和 nil为假，其它都为真
5. function函数
6. table 数组，容器
7. userdata (类，其它语言转换过来就变成userdata类)
9. thread 线程

## Lua GC
> 在Lua5.1后，lua采用分布回收以及三色增量标记清除算法，基本原里：

* 每个新创建的对象设置为白色
* 遍历root节点中引用的对象，从白色置为灰色，并且放入到灰色节点链表中
* 从灰色链表中取未扫描到的对象，将其置为黑色，遍历这个对象关联的其他所有对象：如果为白色，则标记为灰色并加入到灰色链表中
* 遍历所有对象，如果是白色，执行灰色，否则塞入到对象链表中，等待下一轮GC


