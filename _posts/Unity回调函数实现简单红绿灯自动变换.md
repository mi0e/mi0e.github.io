---
layout: post
cid: 133
title: Unity回调函数实现简单红绿灯自动变换
slug: 133
date: 2022/10/27 21:24:00
updated: 2022/10/27 21:25:17
status: publish
author: mi0e
categories: 
  - Unity
tags: 
  - unity
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


```c#
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class AutoChangeColor : MonoBehaviour
{
    public Material[] color;
    int i = 0;
    MeshRenderer meshRenderer;
    void Start()
    {
        meshRenderer = GetComponent<MeshRenderer>();
        ChangeColor();
    }

    void Update()
    {

    }

    private void ChangeColor()
    {
        meshRenderer.material = color[i];
        if (i == 0) Invoke("ChangeColor", 3);
        else if(i == 1) Invoke("ChangeColor", 1);
        else if(i == 2) Invoke("ChangeColor", 3);
        i += 1;
        if (i == 3) i = 0;
    }
}

```
