---
layout: post
cid: 102
title: IMG数组相关
slug: 102
date: 2022/09/24 11:43:00
updated: 2022/09/24 12:16:47
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


图片ROI区域选取：`img[0:100,0:100]`

```python
img[垂直区域, 水平区域, 颜色通道]
```

注：`cv2.imread()`读取顺序是BGR

---

取单通道值：

```python
# 将G,B通道写入0
img[:,:,0] = 0
img[:,:,1] = 0
```

垂直翻转：`img[::-1,:]`

水平翻转：`img[:,::-1]`
