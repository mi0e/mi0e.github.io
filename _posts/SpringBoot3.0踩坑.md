---
layout: SpringBoot踩坑
title: SpringBoot踩坑(1)
date: 2023-05-06 22:13:28
tags:
---

## `import javax.servlet.*;`报错

这个报错主要是Spring Boot3.0已经为所有依赖项从 Java EE 迁移到 Jakarta EE API，导致 servlet 包名的修改，Spring团队这样做的原因，主要是避免 Oracle 的版权问题，解决办法很简单，两步走：

```typescript
// 修改前：
import javax.servlet.*
// 修改后：
import jakarta.servlet.*
```
