---
layout: post
title: "子空间分析与跟踪（3） —— 子空间方法"
description: "子空间分析与跟踪（3） —— 子空间方法"
categories: [Math]
tags: [Notes, 《矩阵分析与应用》, MatrixAnalysis]
redirect_from:
  - /2022/02/13/
---

<head>
    <script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({
            tex2jax: {
            skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'],
            inlineMath: [['$','$']]
            }
        });
    </script>
</head>

- 目录
{:toc}

<!-- # 子空间方法 -->

## 一些基础概念及符号表示

> 在工程应用中，多数情况下使用列空间。

观测数据矩阵$A$不可避免地存在观测误差或噪声。令

$$
X=A+W={x_1,x_2,...,x_n}\in\mathcal{C}^{m\times n}
$$

为观测数据矩阵，其中$x_i\in\mathcal{C}^{m\times 1}$为观测数据向量，而$W$表示加性观测误差矩阵。

在信号处理和系统科学等领域中，

- 观测数据矩阵的列空间称为**观测数据空间**：

$$
Span(X)=Span\{x_1,x_2,...,x_n\}
$$

- 观测误差矩阵的列空间称为**噪声子空间**：

$$
Span(W)=Span\{w_1,w_2,...,w_n\}
$$

## 信号子空间与噪声子空间

- 相关矩阵

$$
R_X=E\{X^HX\}=E\{(A+W)^H(A+W)\}
$$

如果假设误差矩阵与真实数据矩阵$A$统计不相关，上式可以进一步化简得到

$$
\begin{aligned}
    R_X&=E\{X^HX\}=E\{(A+W)^H(A+W)\}\\&=E\{A^HA\}+E\{W^HW\}
\end{aligned}
$$

如果，$R=E\{A^HA\},E\{W^HW\}=\sigma_w^2I,rank(A)=r$，则有

$$
\begin{aligned}
    R_X&=R+\sigma_w^2I=U\Lambda U^H+\sigma_w^2I\\&=U(\Lambda+\sigma_w^2I)U^H=U\Pi U^H
\end{aligned}
$$

其中

$$
\Sigma=diag(\sigma_1^2,...,\sigma_r^2,0,...,0)\\
\Pi=\Lambda+\sigma_w^2I=diag(\sigma_1^2+\sigma_w^2,...,\sigma_r^2+\sigma_w^2,\sigma_w^2,...,\sigma_w^2)
$$

且 $\sigma_1^2\ge\sigma_2^2\ge...\ge\sigma_r^2$

如果**信噪比足够大**（$\sigma_r^2$>>$\sigma_w^2$），那么

- **主特征值**（principal eigenvalue）：含噪声的自相关矩阵$R_X$的前r个大特征值

$$
\begin{matrix}
    \lambda_i=\sigma_i^2+\sigma_w^2,&i=1,...,r
\end{matrix}
$$

- **次特征值**（minor eigenvalue）：除了主特征值以外的$n-r$个小特征值

$$
\begin{matrix}
    \lambda_i=\sigma_w^2,&i=r+1,...,n
\end{matrix}
$$

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220213154650.png"/></div>

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220213154748.png"/></div>

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220213160536.png"/></div>

### 信号子空间和噪声子空间的几何意义

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220213160715.png"/></div>

## 主分量分析(principal component analysis, PCA)和次分量分析(minor component analysis, MCA)

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220213161051.png"/></div>

## 子空间应用的几个特点

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220213161026.png"/></div>

---

[1] 张贤达. (2004). 矩阵分析与应用. 清华大学出版社有限公司.
