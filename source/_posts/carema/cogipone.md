---
title: VisionPro预处理工具之一(CogIPOneImageTool)讲解
categories:
  - 视觉
  - CogIPOneImageTool
tags:
  - 视觉
comments: true
toc: false
donate: true
share: true
source: https://blog.csdn.net/syzmbao/article/details/141218315
date: 2024-10-29 11:26:08

---

CogIPOneImageTool工具主要用来对单张图像进行算法处理操作，多用于拍摄的图片特征不够突出或者难以定位、卡尺卡边、斑点工具颜色难以分辨等，是很好用的一个[预处理](https://so.csdn.net/so/search?q=%E9%A2%84%E5%A4%84%E7%90%86&spm=1001.2101.3001.7020)工具。

### ******添加图像与工具******

![](https://i-blog.csdnimg.cn/direct/9ad95e8e5b10442395d084899432535b.png)

![](https://i-blog.csdnimg.cn/direct/a634f99513234124b168684c051afcbb.png)

### ******参数介绍:******

![](https://i-blog.csdnimg.cn/direct/c71e3f5384294fc8831bda83459e1153.png)

#### ******加减常量******

为[灰度图像](https://so.csdn.net/so/search?q=%E7%81%B0%E5%BA%A6%E5%9B%BE%E5%83%8F&spm=1001.2101.3001.7020)中每个像素的灰度值添加正值或负值，从而生成一张更亮或更暗的图像

![](https://i-blog.csdnimg.cn/direct/41e38f4f1204464faede2ccb5d42bd7d.png)![](https://i-blog.csdnimg.cn/direct/049f2db9304846b7a930a5c2b05421c0.png)![](https://i-blog.csdnimg.cn/direct/2e3dec7387144205bb9912b35b191e26.png)![](https://i-blog.csdnimg.cn/direct/17e5612fe45443aa8dfaff38e0bd8bc7.png)

##### ******封装******

超出255亮度的像素会执行减去256的操作，小于0的会执行加256的操作  

##### ******箝位******

最高到255的亮度，最小到 0

 ![](https://i-blog.csdnimg.cn/direct/a6961c21b418414e9f91eaba9ca3ea21.png)![](https://i-blog.csdnimg.cn/direct/b56a5b449a1b4cff909be0fb6fdd1a3c.png)

##### ******平面********0:********,平面1********:********,平面********2:******

****R********gb****  ****红绿蓝****

![](https://i-blog.csdnimg.cn/direct/49f551ba8bfb45b2b8b94d45750d9d75.png)

![](https://i-blog.csdnimg.cn/direct/5534161c50bb40278a795f58e9ad7515.png)

![](https://i-blog.csdnimg.cn/direct/e736fd1000d745e6a74b893f0bc3bc24.png)

![](https://i-blog.csdnimg.cn/direct/4585b8a77f8e41338e3dc1774875b536.png)

#### ******卷积******

VisionPro支持卷积运算符，基于相邻像素值修改像素值。VisionPro将输入图像中的每个像素乘以一个称为****核****的数值矩阵，然后替换输出图像中的相应像素。不同卷积核可以实现不同的效果，比如平滑、模糊、去噪、锐化、 边缘提取等，都可以通过卷积操作来完成

通过3\*3卷积核的矩阵运算 计算完成后

替换原有的像素

![](https://i-blog.csdnimg.cn/direct/f8df26245cd54c1db3a38e546b4e01f9.png)

卷积核效果参考网址：

[https://setosa.io/ev/image-kernels/](https://setosa.io/ev/image-kernels/ "https://setosa.io/ev/image-kernels/")

 ![](https://i-blog.csdnimg.cn/direct/0858adeeef664e11882848bfcd89f3e6.png)

![](https://i-blog.csdnimg.cn/direct/0070a4f4a7da4a34b4ab820b0e052860.png)

经过卷积操作的图像变得模糊

卷积 3x3 运算符可用于锐化图像的边缘

![](https://i-blog.csdnimg.cn/direct/7aeaa4950dad4e48b049563c40663f81.png)

![](https://i-blog.csdnimg.cn/direct/428877cf513d46dcbbcf328dad8b9c6f.png)

![](https://i-blog.csdnimg.cn/direct/225e96833fd8441bb21025d67cd4a52b.png)

#### ******均衡******

直方图均衡化 (Histogram Equalization)是一种增强图像对比度 (Image Contrast)的方法，其主要思想是将一副图像的直方图分布变成近似均匀分布， 从而增强图像的对比度。过暗和过亮的图像经过直方图均衡化，图像会变得清晰。

![](https://i-blog.csdnimg.cn/direct/970167206d1f40fe93462b1e6571a3dd.png)

应用说明： 当生产环境中的照明在一个图像到另一个图像之间可能略有变化时， 或者在要检查的对象的某些方面（例如颜色）略有变化时，就需要使用均衡操作。 均衡操作有助于确保生产环境中不相关的更改不会影响视觉应用的整体结果 

![](https://i-blog.csdnimg.cn/direct/5a6a0da5ed074b86a8441b4996919200.png)

![](https://i-blog.csdnimg.cn/direct/918b7923c4544bf6b09d3df82022f77f.png)

设置过均匀之后会发现[灰度值](https://so.csdn.net/so/search?q=%E7%81%B0%E5%BA%A6%E5%80%BC&spm=1001.2101.3001.7020)变多,分布更均匀

#### ******扩展******

用指定的放大倍数放大整个图像或整个图像的一部分。

该操作接受单独的参数以沿x轴和y轴放大图像，因此可以使用该操作仅沿一个方向放大输 入图像。

例如，下图显示了输入图像以及放大5倍后的图像

![](https://i-blog.csdnimg.cn/direct/bb822e4f08394658adda5f86336b2a1d.png)

![](https://i-blog.csdnimg.cn/direct/f23c7af8bbc942c79f811d95a5760812.png) 

#### ******旋转******

对输入图像的全部或部分执行水平翻转或顺时针旋转。下图显示了输入图像 的一部分如何旋转180度。您可能需要翻转或旋转图像，以便视觉工具在每次应 用程序执行时分析正确的功能

 ![](https://i-blog.csdnimg.cn/direct/3c92cab9902f462bb1eb74d7b1da053f.png)

![](https://i-blog.csdnimg.cn/direct/7af911ffad484d6a8cd9b19131b27e25.png)

![](https://i-blog.csdnimg.cn/direct/9fbb9c71da7b4c02b8da06cd760d52b4.png)

#### ******高斯采样器******

对输入图像进行子采样，以使输出图像仅包含原始像素的一小部分，并平滑图像

（1）当视觉工具在缩小的图像上同样有效地工作并且想要提高应用程序的速度时， 可使用采样操作。 例如2\*2 图像缩小一倍

（2）使用平滑操作可减轻图像中纹理，信号噪声等带来的影响。

（3）可调整幅度偏移因子，范围为-7至7。 使用负值作为移位因子可产生较暗的输出图像，而使用正值可产生较亮的输出图像。

 ![](https://i-blog.csdnimg.cn/direct/b7947598ea98487a92c0eb7d69a81524.png)

![](https://i-blog.csdnimg.cn/direct/6df06496f05e47aa9862142e952d09ac.png)

#### ******形态学调整******

对输入图像执行灰度形态，根据其大小和方向有选择地增强或减少图像特征。

形态运算符使用结构元素定义的边界（高3像素，宽3像素）检查每个像素及其 八个相邻像素的灰度值

![](https://i-blog.csdnimg.cn/direct/befaa775b9c1445d9534d86357989cf7.png)

##### ******腐蚀******

侵蚀会降低图像的亮点，从而完全消除噪点像素或小的缺陷

![](https://i-blog.csdnimg.cn/direct/99896063a144422b8508022edbb3ad8e.png)

##### ******膨胀******

增强了图像的明亮特征，同时抑制了较暗的特征

![](https://i-blog.csdnimg.cn/direct/9b19aa46b4654246bfefac208bcf8a82.png)

##### ******打开******

打开(开运算)open：首先对输入图像进行腐蚀，然后对结果进行膨胀，以生成输出图像。打开图像会删除少量明亮像素，然后增强其余的明亮功能

![](https://i-blog.csdnimg.cn/direct/c3552dd556ce4dacaa1b846428156c89.png)

##### ******关闭******

关闭(闭运算)close：首先对输入图像执行膨胀，然后对结果进行腐蚀以生成输出图像。关闭图像可减少或完全消除图像的暗区

![](https://i-blog.csdnimg.cn/direct/99bf124dfe404ece844ddb3c2d8206ce.png)

****打开和关闭操作符都倾向于保留大特征的尺寸和形状，同时影响小特征的尺寸和形状****

![](https://i-blog.csdnimg.cn/direct/07cfe6a9d3cf4da7a2ccf81843d392f9.png)

![](https://i-blog.csdnimg.cn/direct/d2b85453fcc246489031ce822969bc26.png)

####
