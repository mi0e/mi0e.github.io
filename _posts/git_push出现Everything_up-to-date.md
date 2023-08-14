---
layout: post
cid: 91
title: git push出现Everything up-to-date
slug: 91
date: 2022/05/22 18:45:19
updated: 2022/05/22 18:45:19
status: publish
author: mi0e
categories: 
  - 编程
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


## 原因：

没有添加文件

## 解决方法：

```
git add .
git commit -m "commit"
git push origin master
```
