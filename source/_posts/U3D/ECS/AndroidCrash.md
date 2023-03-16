---
title: Android 常见 Crash
categories: U3D
tags: 其它
date: 2021-08-30 12:00:00
toc: true
---

# Android Crash

[Android官网检测和诊断崩溃问题](https://developer.android.com/games/optimize/crash?hl=zh-cn)

Android 6.0的源码剖析[理解Android Crash处理流程](http://gityuan.com/2016/06/24/app-crash/)

[unity crash 的快速定位](https://zhuanlan.zhihu.com/p/77984555)

基本概念：

* ANR 

用户在使用App过程中出现弹框，提示应用无响应，计为一次ANR，ANR仅用于Android平台应用。

* Java Crash

Java 崩溃就是在 Java 代码中，出现了未捕获异常，导致程序异常退出，Jvm虚拟机退出，系统弹框提醒用户，这个我们可以看log查看报错原因，Crash工具都能捕获到。

* Native Crash

那 Native 崩溃一般都是因为Native代码中访问非法地址或者是地址对齐出现问题，再或者是发生程序主动abort，这些都会产生对应的signal信号，导致程序异常退出

* SIGSEGV 

一般是由于空指针、非法指针造成

* SIGABRT

后者主要因为 ANR 和调用abort()退出所导致。

# Crash常见原因

* OOM
  
  代码层或资源内存泄漏

* NullPointerException 

  空指针异常

* IndexOutOfBoundsException

  数组、集合等越界

* java.lang.StackOverflowError 

  堆栈溢出错误。当一个应用递归调用的层次太深而导致堆栈溢出时抛出该错误，（死循环了等）

* ClassCastException 

  类型转换异常 

* ActivityNotFoundException 
   
  Activity未找到异常

* SecurityException 

  安全异常 

* llegalArgumentException: Service not registered 

  服务未注册异常 
  
* BadTokenException

* API 平台兼容性
  Unity 的一些API在不同硬件的兼容性问题

## 错误符号
1. SIGSEGV 段错误

   SEGV_MAPERR	要访问的地址没有映射到内存空间。 比如上面对空指针的写操作， 当指针被意外复写为一个较小的数值时。

   SEGV_ACCERR	访问的地址没有权限。比如试图对代码段进行写操作。

2. SIGFPE 浮点错误，一般发生在算术运行出错时。

   FPE_INTDIV	除以0

   FPE_INTOVE	整数溢出

3. SIGBUS 总线错误
   BUS_ADRALN	地址对齐出错。arm cpu比x86 cpu 要求更严格的对齐机制，所以在 arm cpu 机器中比较常见。

4. SIGILL 发生这种错误一般是由于某处内存被意外改写了。

   ILL_ILLOPC	非法的指令操作码

   ILL_ILLOPN	非法的指令操作数

5. 当调用堆栈中出现 stack_chk_fail 函数时，一般是由于比如 strcpy 之类的函数调用将栈上的内容覆盖，而引起栈检查失败。

![枚举](/images/crash/Signum.jpeg)

### 分类

> 一般分为Java Crash 和 Native Crash

## Native Crash

### 特点
1. 出错时界面不会弹出提示框提醒程序崩溃（Android 5.0以下）
2. 出错时会弹出提示框提醒程序崩溃（Android 5.0以上）
3. 程序会直接闪退到系统桌面
4. 这类错误一般是由C++层代码错误引起的
5. 绝大部分Crash工具不能够捕获

### 产生原因

# 崩溃分析

1. 堆栈信息查找
2. log日志，尤其是warning error相关
3. 机型信息  GPU 内存 系统 厂商 信息等共性信息，(有可能某个厂商特定修改)
4. 复现步骤
5. 前后台信息

  
# 工具

addr2line，objdump，ndk-stack等几个工具


# 问题记录

