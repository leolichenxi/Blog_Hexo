---
title: GoogleProtobuffer
categories: Tools
tags: GoogleProtobuffer
date: 2021-06-14 12:00:00
toc: true
---

# Protocolbuffers

* [官方git地址](https://github.com/protocolbuffers/protobuf)
* [官方文档地址](https://developers.google.com/protocol-buffers)
* [官方Release](https://github.com/protocolbuffers/protobuf/releases)
* [知乎介绍](https://zhuanlan.zhihu.com/p/38200420)

Protocol Buffers 是一种轻便高效的结构化数据存储格式，可以用于结构化数据串行化，很适合做数据存储或 RPC 数据交换格式。它可用于通讯协议、数据存储等领域的语言无关、平台无关、可扩展的序列化结构数据格式。

常见的数据格式：XML,Json,Protobuf,FlatBuffers 等其它。

* 数据储存
* 数据交换格式

使用流程：

1.编写Scheme;
2.使用Protoc 生成代码；

## 下载Release Protoc代码生成工具

> Release中下载Window 或 Mac Os
![截图](/images/protobuffer/1.png)

### 设置环境变量

在下载程序后，需要将下载 zip 文件中的 bin 目录设置到环境变量中。

然后运行 protoc --version 来确定你的编译运行版本已经被正确配置。

### 使用

[官方文档地址](https://developers.google.com/protocol-buffers)

生成代码命令

> eg:   protoc -- csharp_out=SciptOutFolder/  ProtoFolder/filename.proto


### Protocol Buffer 编码原理

采用Varint编码规则

#### Varint编码

variant是可变长的编码方式,Varint是一种使用一个或多个字节序列化整数的方法，会把整数编码变为长字节，对于32位整型进过Variant编码后需要1-5个字节,小的数字使用1个byte，大的数字使用5个bytes。64位整型数据编码后占用1~10个字节。在实际场景中小数字的使用率远远大于大数字，因此Varint编码对于大部分的场景都可以起到很好的压缩效果。

##### 编码原理

除了最后一个字节外,Varint编码中的每个字节都设置了最高有效位（most significant bit - msb）–msb为1则表明后面的字节还是属于当前数据的,如果是0那么这是当前数据的最后一个字节数据。每个字节的第7位用于以7位为一组存储数字的二进制补码表示，最低有效组在前，或者叫最低有效字节在前。这表明varint编码后数据的字节是按照小端序排列的。

关于字节排列的方式引用一下维基百科上的词条
> 字节的排列方式有两个通用规则。例如，一个多位的整数，按照存储地址从低到高排序的字节中，如果该整数的最低有效字节（类似于最低有效位）在最高有效字节的前面，则称小端序；反之则称大端序。在网络应用中，字节序是一个必须被考虑的因素，因为不同机器类型可能采用不同标准的字节序，所以均按照网络标准转化。

通俗一点说就是：大端序是按照数字的书写顺序排列的，而小端序是颠倒书写顺序进行排列的。

> variant编码对负数编码效率低