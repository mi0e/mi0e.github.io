---
title: hexo相关（一）
date: 2023-02-13 18:19:31
tags: hexo
---


### 新建markdown文件

```
# cd 根目录
hexo new [filename]
```

### 清理原始文件（配置文档）

```
hexo clean
```

### 渲染md

```
hexo g / hexo generate
```
### 部署到本地服务器

```
hexo s / hexo server
```

### 部署到指定仓库

```
hexo d / hexo deploy
```

### 生成algolia目录并推送

```
# 需提前在git bash配置环境变量
# export HEXO_ALGOLIA_INDEXING_KEY = API key
hexo algolia
```