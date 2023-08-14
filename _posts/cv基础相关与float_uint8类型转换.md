---
layout: post
cid: 100
title: cv基础相关与float/uint8类型转换
slug: 100
date: 2022/09/20 23:37:00
updated: 2022/09/20 23:38:37
status: publish
author: mi0e
categories: 
  - Opencv
tags: 
customSummary: 
mathjax: auto
noThumbInfoEmoji: 
noThumbInfoStyle: default
outdatedNotice: no
parseWay: auto
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


### cv基本

```python
img = cv2.imread("Path")    #打开图片
cv2 = imshow("窗口标题", img)	#显示
```

### resize()

```python
dst = cv2.resize(src,dsize,dst=None,fx=None,fy=None,interpolation=None)
```

* **src**：输入图像
* **dsize**：输出图像的大小。如果该参数为 0，表示缩放之后的大小需要通过公式计算，`dsize = Size(round(fx*src.cols),round(fy*src.rows))`。其中 `fx` 与 `fy` 是图像 Width 方向和 Height 方向的缩放比例。
* **fx**：Width 方向的缩放比例，如果是 0，按照 `dsize * width/src.cols` 计算
* **fy**：Height 方向的缩放比例，如果是 0，按照 `dsize * height/src.rows` 计算
* **interpolation**：插值算法类型，或者叫做插值方式，默认为双线性插值
* 方法返回结果 dst 表示输出图像。

### 相关参数

```python
a=cv2.imread("1.jpg")
print(a.shape[0], a.shape[1], a.shape[2])
```

shape0 : 垂直尺寸

shape1 : 水平尺寸

shape2 : 颜色通道

### 数据类型查看与转换

##### type() ,dtype() ,astype()区别


| 函数     | 说明                                                                                                                                                                                                |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| type()   | 返回数据结构类型（list、dict、numpy、ndarray 等）                                                                                                                                                   |
| dtype()  | 返回数据元素的数据类型（int、float等）<br />备注：<br />1）由于 list、dict 等可以包含不同的数据类型，因此不可调用dtype()函数<br />2）np.array 中要求所有元素属于同一数据类型，因此可调用dtype()函数 |
| astype() | 改变np.array中所有数据元素的数据类型。<br />备注：能用dtype() 才能用 astype()                                                                                                                       |

##### 类型转换

方法1：

```python
# 通过np转换类型后除以255得到float类型
a = a.astype(np.float32)
a/=255.0
print(a)
```

方法2：

```python
# 直接使用skimage转换
a = skimage.img_as_float(a)  #默认为float64，可选img_as_float32
```
