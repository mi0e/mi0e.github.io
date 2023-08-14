---
layout: post
cid: 68
title: img标签在谷歌浏览器下不显示错误信息
slug: 68
date: 2021/11/01 09:00:46
updated: 2021/11/01 09:00:46
status: publish
author: mi0e
categories: 
  - Q/A
tags: 
customSummary: 
mathjax: auto
noThumbInfoStyle: default
outdatedNotice: no
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


添加全局js

```html
<style>
img[src=""],img:not([src]){opacity:0;}
</style>
```
