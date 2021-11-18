---
title: Audio
categories: Audio
tags: 资源
date: 2021-06-14 12:00:00
toc: true
---

导入前的声音格式选择

     短声音：.aifff和.wav

    长声音：.mp3和.ogg

导入后的声音格式选择

     Force ToMono：如果启用，该音频将向下混合到单声道

    Load In Backgroud: 加载将在一个单独的线程上延迟的时间发生，而不会阻塞主线程

    Ambisonic: 如果音频文件包含有双声编码的音频，那么启用这个选项 

    LoadType: ①Decompress On Load:处理较小的声音（load就解压）

                      ②Compressed In Memory：较大的声音（保持解压的状态）

                      ③Streaming：使用最少的内存来缓冲压缩数据（很长的音乐）

 Compression Format：

                     ①PCM  非常短的音效是最好的，质量高，文件大

                     ②ADPCM大量噪音的声音，需要大量播放，比如脚步声，武器

                     ③Vorbis/MP3 质量低，中等长度背景音乐

                     ④HEVAG 类似于adpcm

Preload Audio Data 预加载

 

方案：大点的音频: Streaming,不预加载，Vorbis

     小点的音频DecompressOnLoad 不预加载  ，Vorbis

会优化比较适中的cpu和内存，具体还要根据项目实际确定

# Unity性能优化-音频设置

没想到Unity的音频会成为内存杀手，在实际的商业项目中，音频的优化必不可少。

1. Unity支持许多不同的音频格式，但最终它将它们全部转换为首选格式。音频压缩格式有PCM、ADPCM、Vorbis，不是所有平台都支持这些所有的压缩格式，有些平台，例如WebGL只支持AAC格式。

2. 所有音频导入时，默认两项设置，LoadType是"Decompress On Load"，压缩格式是“Vorbis”，例如下图原始文件大小计算为35.9 MB，导入的大小计算为10.7 MB。这意味着这个音频剪辑将使您的游戏（存档）大小增加10兆字节，但播放它需要近36兆字节的RAM。

These are default import settings.

3. Load Type的各个选项

Compressed In Memory – 音频剪辑将存储在RAM中，播放时将解压缩，播放时不需要额外的存储。
Streaming –音频永久存在设备上(硬盘或闪存上) ，播放流媒体方式. 不需要RAM进行存储或播放。
Decompress On Load – 未压缩的音频将存储在RAM中。这个选项需要的内存最多，但是播放它不会像其他选项那样需要太多的CPU电源。
         怎么选？长音频播放消耗大量内存，如果播放时不想在内存中进行解压，有两个选择：

         （1）Load Type选“Streaming”， Compression Format 选”Vorbis"，使用最少的内存，但需要更多的CPU电量和硬盘I/O操作；

         （2）Load Type选“Compressed In Memory”， Compression Format 选”Vorbis"，磁盘I/O操作被替换成内存的消耗，请注意，要调整“Quaility”滑块以减小压缩剪辑的大小，以交换音质，一般推荐70%左右。

             一般是看到底音乐占据多少内存以及你的目标机型是什么样子的，如果音乐占据的内存本身比较高，你的目标机型的内存又比较小，那么就选择第二种，这种方案会卡一点，否则选择第一种就更好

4. 声音特效

     （1）对于经常播放的和短的音频剪辑，使用“Decompress On Load”和“PCM或ADPCM"压缩格式。当选择PCM时，不需要解压缩，如果音频剪辑很短，它将很快加载。你也可以使用ADPCM。它需要解压，但解压比Vorbis快得多。

      （2）对于经常播放，中等大小的音频剪辑使用”Compressed In Memory“和”ADPCM“压缩格式，比原始PCM小3.5倍，解压算法的CPU消耗量不会像vorbis消耗那么多CPU。

      （3）对于很少播放并且长度比较短的声音剪辑，使用”Compressed In Memory", ADPCM 这种压缩格式,原因同（2）。

     （4）对于很少播放中等大小的音频，使用”Compressed In Memory“ 和Vorbis压缩格式。这个音频可能太长，无法使用adpcm存储，播放太少，因此解压缩所需的额外CPU电量不会太多。
