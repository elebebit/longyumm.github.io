---
layout:     post   				    # 使用的布局（不需要改）
title:      深度学习与视频编码 				# 标题 
subtitle:   总结                     #副标题
date:       2019-07-07				# 时间
author:     longyu 						# 作者
header-img: img/post-bg-2015.jpg 	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签
    - 深度学习
    - 视频编码
---


This paper is inspired by Prof. Wang in Peking University.

神经网络视频编码历史:

<center><img src="/_posts/20190707/history.png" width="100%" height="100%" /></center>


**起源：**

基于神经网络的编码技术源自于上世纪八十年代

<center><img src="20190707/3-layer-pm.png" width="40%" height="40%" /></center>

<center>三层人工神经网络用于图像变换编码~[refer](https://www.semanticscholar.org/paper/Image-compression-by-back-propagation%3A-A-of-Cottrell-Munro/6db399b4afd41d29c06bbb88c1de370a4b93f994)</center>

**上世纪九十年代初：**

基于多层感知机的图像编码

- DPCM using a multilayer preceptron network

<center><img src="https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/4438acc36941128ab8268e5c5a3c4daa693c9529/5-Figure5-1.png" width="40%" height="40%" /></center>

- Predictive Coding

<center><img src="20190707/predictive_coding.png" width="40%" height="40%" /></center>

**九十年代中期：**

自适应预测编码

- Complexity analysis & Entropy coding 

<center><img src="20190707/comple_analy.png" width="40%" height="40%" /></center>
<center>将图像划分为小块进行编码</center>

<center><img src="20190707/entroy_code.png" width="40%" height="40%" /></center>
<center>利用空域临近像素作为辅助预测</center>

**2000年左右**

1.端到端的多层感知机编码

2.由图像扩展到视频编码

<center><img src="20190707/pic2video.png" width="60%" height="60%" /></center>

**2006**

自编码开启深度学习时代 By G.E. Hinton

<center><img src="20190707/auto_codec.png" width="60%" height="60%" /></center>

---

###基于深度学习的视频编码进展:

#####深度学习与视频编码

- <font color="#3500b2">帧内预测</font>
- <font color="#3500b2">帧间预测</font>
    + <font color="#00cc3d">分像素插值</font>
    + <font color="#00cc3d">预测增强</font>
    + <font color="#00cc3d">参考帧质量提升</font>
- <font color="#3500b2">环路滤波</font>
- <font color="#3500b2">模式决策</font>
    + <font color="#00cc3d">编码优化</font>


**帧内预测：**

<i class="far fa-star"></i> 数据驱动的帧内预测方法

- 基于全卷积网络
- 全连接网络
    + 单一模型：IPFCN-S(IPFCN-S-L:将网络参数减半)
    + 双模型(为DC和planar训练专门模型)：IPFCN-D(IPFCN-D-L:将网络参数减半)

<center><img src="https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/c18a866a8c2992e1307eba67d7aeba9155bf1e11/4-Figure2-1.png" width="60%" height="60%" /></center>
<center>[IPFCN](https://ieeexplore.ieee.org/document/8319436)</center>


<i class="far fa-star"></i> Design Resnet for Intra 8x8 PU
<center><img src="https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/d09c8d9d6b432b852d2295f67e679a460734dba7/4-Figure1-1.png" width="60%" height="60%" /></center>
<center>[Refer](https://ieeexplore.ieee.org/document/7923719)</center>

<i class="far fa-star"></i> 预测增强

- 训练数据生成
- 当前PU通过HEVC得到最优intra mode

<center><img src="20190707/pre-enhance.png" width="60%" height="60%" /></center>

<i class="far fa-star"></i> 残差网络学习

<i class="far fa-star"></i> QP: 22 27 32 37, HEVC Intra, DL Platform: Matcovnet


**帧间预测：**

<i class="far fa-star"></i> 基于深度学习的分像素插值

- 针对1/2像素设计神经网络
    + 帧间预测：分像素插值 + 图像超分

<center><img src="https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/29289657c1f96f3ae948ad6443530a4d5a5679b9/5-Figure3-1.png" width="60%" height="60%" /></center>
<center>[Refer](https://ieeexplore.ieee.org/document/8319451)</center>


<center><img src="https://pigundermoon.github.io/GVCNN/img/net.PNG" width="60%" height="60%" /></center>
<center>[Refer](https://pigundermoon.github.io/GVCNN/GVCNN.html)</center>

<i class="far fa-star"></i> 帧间预测增强

- 利用空域-时域联合信息
    + 空域周边像素重建
    + 时域参考像素

<center><img src="https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/4950fe1f9fedc597218cef63088eb1d9206c8fb9/3-Figure3-1.png" width="60%" height="60%" /></center>
<center>[Refer](https://ieeexplore.ieee.org/document/8486600)</center>

- 提升预测准确性
    + [帧间双向预测（BIP）](https://ieeexplore.ieee.org/document/8493529)

    <center><img src="20190707/bip.png" width="60%" height="60%" /></center>

    + [虚拟参考帧生成](https://ieeexplore.ieee.org/document/8451465)

    <center><img src="https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/5ceb6240f266c2c1ab7aaef9c89f228b328b1c1a/2-Figure1-1.png" width="60%" height="60%" /></center>


**环路滤波**

<i class="far fa-star"></i> 基于整帧的处理：SRCNN

<center><img src="https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/7518124/7528174/7528223/7528223-fig-2-source-large.gif" width="60%" height="60%" /></center>

<center>[SRCNN](https://ieeexplore.ieee.org/document/7528223)</center>


<i class="far fa-star"></i>帧内编码后处理

- Post processing, All Intra
- QP: 22,27,32,37

<center><img src="https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/36d2d7fb483960141c0c55ae781a12bc07b467f2/4-Figure1-1.png " width="60%" height="60%" /></center>

<center>[Refer](https://arxiv.org/abs/1608.06690)</center>

<i class="far fa-star"></i>基于内容特性的神经网络环路滤波

- 针对不同内容特性的视频图像训练CNN模型
- Content analysis + CNN in-loop filter

<center><img src="20190707/content-filter.png" width="60%" height="60%" /></center>
<center>[Refer](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=8630681)</center>

<i class="far fa-star"></i>智能编码与VVC(JVET-N0110)

- ALF之后
- 浅层卷积神经网络
- 亮度分量与色度分量共享网络
- 帧级开关、CTU级开关、32x32块开关

<center><img src="20190707/VVC.png" width="60%" height="60%" /></center>


<i class="far fa-star"></i>智能编码与VVC(JVET-N0133)

- 代替Deblock, SAO, ALF 
- 辅助输入信息：块划分结构和QP
- SE（Squeeze and Excitation）block 


<i class="far fa-star"></i>智能编码与VVC(JVET-N0169)

- CNNLF的位置
- 辅助输入信息：QP Map
- 并行化：分块滤波

<i class="far fa-star"></i>智能编码与VVC(JVET-N0254)

- Dense Residual CNN 
- 深度可分离卷积（DSC）减少参数量

<i class="far fa-star"></i>智能编码与AVS3

- QP分段训练残差网络
- 代替Deblock,SAO,ALF
- 帧级开关、CTU级开关

**帧内编码模式决策**

<i class="far fa-star"></i>基于CNN的CU模式决策

- 分析CU块纹理
- 减少CU模式的数目
- 引入QP作为辅助信息

<i class="far fa-star"></i>实现

- Adding FastCUMode()
- into xCompressCU

<center><img src="https://ai2-s2-public.s3.amazonaws.com/figures/2017-08-08/ecaa4d9d455ed86c50cff910a1c7bd34b49fda5f/1-Figure1-1.png" width="60%" height="60%" /></center>
<center>[Refer](https://ieeexplore.ieee.org/document/7539036)</center>


<i class="far fa-star"></i>HEVC Intra 硬件编码器实现

- Big/Small CU pipeline


<i class="far fa-star"></i>使用类似LeNet结构

<center><img src="https://www.jqr.com/editor/319/947/3199471286-5b236d810edba" width="60%" height="60%" /></center>
<center>[Refer](https://ieeexplore.ieee.org/document/7539036)</center>


<i class="far fa-star"></i>将编码模型决策建模为二分类问题

- 预测当前编码单元是否划分

<i class="far fa-star"></i>VLSI设计CNN加速模块

**下采样-上采样编码**

<i class="far fa-star"></i>CTU级处理

- 两级RDO
    + 是否采用变分辨率编码
    + 上采样模块使用DCT插值或CNN

<center><img src="https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/76/8466125/7982641/liu1-2727682-hires.gif" width="60%" height="60%" /></center>
<center>[Refer](https://ieeexplore.ieee.org/document/7982641)</center>


- 亮度分量网络
    + Input: low resolution patch, output: high resolution

<center><img src="https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/76/8466125/7982641/liu2-2727682-hires.gif" width="60%" height="60%" /></center>

- 色度分量处理：使用亮度作为引导

<center><img src="https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/76/8466125/7982641/liu3-2727682-hires.gif" width="60%" height="60%" /></center>


- 算法命中率
    + 绿色：下采样编码+CNN，红色：上采样编码+DCTIF


<center><img src="https://ieeexplore.ieee.org/mediastore_new/IEEE/content/media/76/8466125/7982641/liu9abcd-2727682-hires.gif" width="60%" height="60%" /></center>







<head> 
    <script defer src="https://use.fontawesome.com/releases/v5.0.13/js/all.js"></script> 
    <script defer src="https://use.fontawesome.com/releases/v5.0.13/js/v4-shims.js"></script> 
</head> 
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.0.13/css/all.css">



















