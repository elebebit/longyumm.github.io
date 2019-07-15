---
layout:     post                    # 使用的布局（不需要改）
title:      移动端音视频直播入门             # 标题 
subtitle:   课程内容                    #副标题
date:       2019-07-15              # 时间
author:     longyu                      # 作者
header-img: img/post-bg-android.jpg     #这篇文章标题背景图片
catalog: true                       # 是否归档
tags:                               #标签
    - 音频编码
    - 视频编码
---

[课程链接](https://www.imooc.com/learn/959)


## 1. 万人直播架构讲与CDN入门

### 1.1 万人直播架构讲解

泛娱乐化直播

- 花椒、斗鱼等娱乐游戏直播

实时互动直播

- 音视频会议、教育直播等，对实时性比较高

**泛娱乐化直播架构**

<center><img src="/img/in_post/20190715/live1.png" width="50%" height="50%" /></center>

1. 主播端发起创建房间信令，服务器返回一个流媒体云地址提供服务，主播可以把视频通过rtmp流推送到CDN。 
2. 观众想要观看，通过发送信令，服务器提供CDN地址供观众进行拉流。


**实时互动直播架构**

<center><img src="/img/in_post/20190715/live2.png" width="50%" height="50%" /></center>

使用UDP建立自己的网络，来达到实时的目的。

### 1.2 CDN网络

**边缘节点：**用户从边缘节点上获取数据。

**二级节点：**主干网节点，主要用于缓存，减轻源站压力。

**源站：**CP（内容提供方）将内容放到源站

<center><img src="/img/in_post/20190715/CDN.png" width="70%" height="70%" /></center>

不同运营商的资源可以共享，但是用户是先访问自己运营商的资源。

### 1.3 亲手搭建一套简单的直播系统

**搭建流媒体服务：**

- 准备流媒体服务器（Linux 或 Mac）
- 编译并安装Nginx服务
- 配置RTMP服务并启动Nginx服务

[链接](https://www.imooc.com/video/16763)

## 2. 音频入门

### 2.1 音频基础知识

略过

### 2.2 音频的量化与编码

过程：

<center><img src="/img/in_post/20190715/voice.png" width="50%" height="50%" /></center>

模拟数据 -> 采样 -> 量化 -> 编码 -> 数字信号

**量化基本概念：**

采样大小：一个采样用多少bit存放。常用的是16bit

采样率：采样频率8k、16k、32k、44.1k、48k

声道数：单声道、双声道、多声道

**码率计算：**

计算一个PCM音频流的码率：采样率x采样大小x声道数

例如：采样率为44.1KHz，采样大小为16bit，双声道的PCM编码的WAV文件，
它的码率为44.1Kx16x2=1411.2Kb/s

### 2.3 音频压缩技术讲解

- 消除冗余数据
- 哈夫曼无损压缩

音频编码过程：

<center><img src="/img/in_post/20190715/voice-code.png" width="70%" height="70%" /></center>

### 2.4 音频编解码器选型

常见的音频编码器：

OPUS,AAC,Vorbis,Speex,iLBC,AMR,G.711

性能对比：

<center><img src="/img/in_post/20190715/performance.png" width="70%" height="70%" /></center>

### 2.5 AAC讲解

AAC LC:(Low Complexity)低复杂度，码流128k

AAC HE: AAC LC + SBR (Spectral Band Replication)

AAC HE V2: AAC LC + SBR + PS (Parametric Stereo)

## 3. 视频入门

主要内容参见：[链接](https://longyumm.github.io/2019/07/09/H264_theory/)

### 3.1 视频基本知识

I帧：关键帧，采用帧内压缩技术

B帧：向前参考帧，压缩时只参考前一帧，属于帧间压缩技术

P帧：双向参考帧，压缩时既参考前一帧也参考后一帧，帧间压缩技术

GoP： 视频压缩帧序列组。

- SPS：Sequence Parameter Set,序列参数集，存放帧数、参考帧数目、解码图像尺寸、帧场编码模式选择标识等
- PPS：Picture  Parameter Set,图像参数集，存放熵编码模式选择标识、片组数目、初始量化参数和去方块滤波系数调整标识等

### 3.2 H264编码原理

- 帧内预测压缩，解决的是空域数据冗余问题
- 帧间预测压缩，解决的是时域数据冗余问题
- 整数离散余弦变换（DCT），将空间上的相关性变为频域上无关的数据进行量化
- CABAC压缩

其他部分略过

### 3.3 视频压缩技术详解

略过

### 3.4 H264结构与码率

分层
- NAL层：Network Abstraction Layer, 视频数据网络抽象层
- VCL层：Video Coding Layer, 视频数据编码层

其他部分略过

### 3.5 YUV讲解

- Y表示明亮度，也就是灰阶值，它是基础信号
- U和V表示的是色度，UV的作用是描述影像色彩及饱和度，它们用于指定像素的颜色

其他部分略过






















