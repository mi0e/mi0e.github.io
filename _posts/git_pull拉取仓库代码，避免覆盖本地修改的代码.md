---
layout: post
cid: 89
title: git pull拉取仓库代码，避免覆盖本地修改的代码
slug: 89
date: 2022/05/21 10:46:00
updated: 2022/05/21 10:48:28
status: publish
author: mi0e
categories: 
  - Linux
tags: 
  - github
customSummary: 
mathjax: auto
noThumbInfoEmoji: 
noThumbInfoStyle: default
outdatedNotice: no
parseWay: auto
reprint: internet
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---

```
# 1. 先将本地代码放到暂存区

    git stash​​

# 2. 将远程github（码云等）上面的代码拉取下来

    git pull​​

# 3. 将第一步暂存区的代码放回本地

    git stash pop​​
```