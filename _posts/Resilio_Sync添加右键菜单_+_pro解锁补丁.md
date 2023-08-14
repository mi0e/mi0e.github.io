---
layout: post
cid: 22
title: Resilio Sync添加右键菜单 + pro解锁补丁
slug: 22
date: 2021/01/17 22:48:00
updated: 2021/01/29 18:32:51
status: waiting
author: mi0e
categories: 
  - 教程
tags: 
  - Resilio Sync
customSummary: 
noThumbInfoStyle: default
outdatedNotice: no
reprint: standard
thumb: 
thumbChoice: default
thumbDesc: 
thumbSmall: 
thumbStyle: default
---


最近一直在使用Resilio Sync来下载资源 ::aru:thumb:: ，但发现安装有右键没有同步选项，查阅[官方文档][1]，找到了两种解决方法：

 - CMD添加(ShellExtensionPath.dll)

根据官方文档显示，其根目录下ShellExtensionPath.dll为关键拓展，所以我们只需在CMD命令下使用regsvr32为其重新注册dll，命令如下：
    regsvr32 /i "*\ShellExtensionPath86_*.dll"
[scode type="share"]需注意的是，"" 里是Resilio Sync根目录地址，如果是64位的，将有两个Sync shell扩展：x64和x86，且下画线后每个用户的编码都不一样。[/scode]
![官网文档截图][2]

 - 手动添加注册表

将键值改为1，路径如下：

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System\EnableLUA

----------
[collapse status="false" title="补丁"]补丁链接：[蓝奏云][3]
使用方法：设置-许可证-应用许可证[/collapse]


  [1]: https://help.resilio.com/hc/en-us/articles/206214625-No-Sync-icons-in-the-file-browser-no-Sync-related-items-in-the-context-menu-on-Mac-Windows
  [2]: https://i.loli.net/2021/01/17/VQcMI9EhS28RBK4.png
  [3]: https://wwa.lanzous.com/iPHkHkimpte