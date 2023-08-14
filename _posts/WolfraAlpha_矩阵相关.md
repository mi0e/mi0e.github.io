---
layout: post
cid: 135
title: WolfraAlpha 矩阵相关
slug: 135
date: 2022/10/31 16:28:00
updated: 2022/10/31 16:29:17
status: publish
author: mi0e
categories: 
  - 其他
tags: 
  - WolfraAlpha
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
math: true
---


+,\*, ^, **...** **—** 按元素自动作用

Dot **—** 矩阵积，自动处理行向量和列向量

---

Inverse **—** 矩阵逆 (线性系统用 LinearSolve)

MatrixRank **—** 矩阵的秩

NullSpace **—** 跨越矩阵零空间的向量

RowReduce **—** 行简化阶梯形

PseudoInverse **—** 方阵或矩形矩阵的伪逆

---

Transpose **—** 转置($m^T$，用`esc` tr `esc`)

ConjugateTranspose **—** 共轭转置($m^+$，用`esc` ct `esc`)

LowerTriangularize, UpperTriangularize **—** 提取矩阵的下三角形或上三角形部分

Symmetrize **—** 找出矩阵的对称、反对称等部分

---

Diagonal **—** 获取对角线上的元素列表

Tr **—** 矩阵的迹

Det **—** 行列式

Norm **—** 算子范数，p 范数和 Frobenius 范数

Adjugate **—** 转置伴随

Minors **—** 子式矩阵

Permanent **—** 积和式

---

KroneckerProduct **—** 矩阵的直积 (外积)

---

MatrixPower **—** 数值矩阵或符号矩阵的幂

MatrixExp **—** 矩阵指数

MatrixLog **—** 矩阵对数

MatrixFunction **—** 一般矩阵函数

---

Eigenvalues, Eigenvectors **—** 具体或近似的特征值或特征向量

Eigensystem **—** 特征值和特征向量

CharacteristicPolynomial **—** 符号的特征多项式

> 转自官方文档 [https://reference.wolfram.com/language/guide/MatrixOperations.html.zh](https://reference.wolfram.com/language/guide/MatrixOperations.html.zh)
