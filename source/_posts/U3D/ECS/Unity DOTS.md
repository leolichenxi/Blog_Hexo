---
title: Unity DOTS
categories: DOTS Job
tags: 框架
date: 2021-08-30 12:00:00
toc: true
---

# Job System

[官方文档](file:///D:/Program%20Files/2020.3.14f1c1/Editor/Data/Documentation/en/Manual/JobSystem.html)

1. 借助 Unity C# 作业系统，用户可以编写与 Unity 其余部分良好交互的多线程代码，并使编写正确代码变得更加容易。

2. 编写多线程代码可以带来高性能优势，包括显著提高帧率。将 Burst 编译器与 C# 作业配合使用可以提高代码生成质量，还可以大大降低移动设备的电池消耗。

3. C# 作业系统的一个重要特点是它与 Unity 内部使用的系统（Unity 的原生作业系统）相集成。用户编写的代码与 Unity 共享工作线程。此协作避免了创建超过 CPU 核心数的线程（这种情况会导致争用 CPU 资源）


### NativeContainer

> NativeContainer是一种托管值类型，为本机内存提供了一个相对安全的C#封装器。它包含一个指向非托管分配的指针。与Unity C# 作业系统一起使用时，NativeContainer允许Job 访问与主线程共享的数据，而不是使用副本。

* NativeList - 可调整大小的 NativeArray。
* NativeHashMap - 键/值对。
* NativeMultiHashMap - 每个键有多个值。
* NativeQueue  - 先进先出 (FIFO) 队列。

### NativeContainer Allocator

>创建 NativeContainer 时，必须指定所需的内存分配类型。分配类型取决于作业运行的时间长度。因此，可以定制分配以便在每种情况下获得最佳性能。可以使用三种 Allocator 类型进行 NativeContainer 内存分配和释放。在实例化 NativeContainer 时需要指定适当的一种类型。

* Allocator.Temp 具有最快的分配速度。此类型适用于寿命为一帧或更短的分配，不应该使用Temp将NativeContainer 分配传递给Job，在方法调用返回之前，还需要调用Dispose方法。

以下错误 不应该使用Temp将NativeContainer 分配传递给Job
```
public struct JobSum : IJob
{
    public int a;
    public int b;
    public NativeArray<int> result;
    public void Execute()
    {
        result[0] =  result[0]+ a + b;
    }
}
    void Test()
    {
        JobSum jobSum = new JobSum();
        jobSum.a = 1;
        jobSum.b = 10;
        
        NativeArray<int>  result = new NativeArray<int>(1, Allocator.Temp );
        jobSum.result = result;
        var handle =  jobSum.Schedule();
        handle.Complete();
        result.Dispose();
    }
```

* Allocator.TempJob的分配速度比Temp慢，但比Persistent快。此类型适用于寿命为四帧的分配，并具有线程安全性，如果没有在四帧内对其执行Dispose,控制台会输出一条从本机代码生成的警告。大多数小作业都使用这种 NativeContainer 分配类型。

* Allocator.Persistent 是最慢的分配，但可以在您所需的任意时间内持续存在，如果有必要，可以在整个应用程序的生命周期内存在。此分配器是直接调用 malloc 的封装器。持续时间较长的作业可以使用这种 NativeContainer 分配类型。在非常注重性能的情况下不应使用 Persistent。
