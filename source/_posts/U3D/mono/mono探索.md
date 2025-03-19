---
title: Mono探索
categories:  U3D
tags: 资源
date: 2025-03-18 11:24:00
toc: true
---

## 什么是Mono编译器

[Mono Wiki](https://zh.wikipedia.org/wiki/Mono)

### 术语

[CLI](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E8%AF%AD%E8%A8%80%E6%9E%B6%E6%9E%84) : 
通用语言基础架构

* [通用类型系统](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E5%9E%8B%E5%88%A5%E7%B3%BB%E7%B5%B1)（Common Type System, CTS）
* [元数据系统](https://zh.wikipedia.org/wiki/%E5%85%83%E6%95%B0%E6%8D%AE_(CLI))（Metadata）
* [通用语言规范](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E8%AF%AD%E8%A8%80%E8%A7%84%E8%8C%83)（Common Language Specification, CLS）
* [虚拟执行系统](https://zh.wikipedia.org/wiki/%E8%99%9B%E6%93%AC%E5%9F%B7%E8%A1%8C%E7%B3%BB%E7%B5%B1)（Virtual Execution System, VES）
* [通用中间语言](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E4%B8%AD%E9%97%B4%E8%AF%AD%E8%A8%80)（Common Intermediate Language, CIL）
* 框架（Framework）

[CLR](https://zh.wikipedia.org/wiki/%E9%80%9A%E7%94%A8%E8%AA%9E%E8%A8%80%E9%81%8B%E8%A1%8C%E5%BA%AB) : 通用语言运行库

[LLVM](https://zh.wikipedia.org/wiki/LLVM)

> LLVM是一套编译器基础设施项目，为自由软件，以C++写成，包含一系列模块化的编译器组件和工具链，用来开发编译器前端和后端。它是为了任意一种编程语言而写成的程序，利用虚拟技术创造出编译时期、链接时期、执行时期以及“闲置时期”的优化。它最早以C/C++为实现对象，而目前它已支持包括ActionScript、Ada、D语言、Fortran、GLSL、Haskell、Java字节码、Objective-C、Swift、Python、Ruby、Crystal、Rust、Scala[2]以及C#[3]等语言。