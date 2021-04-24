---
layout: post
title: "Matrix Operations in R"
description: "matrix operations, R"
categories: [R]
tags: [R, Operations]
redirect_from:
  - /2021/04/24/
---

```R
x1 <- c(1:20) #创建一个向量，无特殊说明向量都是列向量，x1为（1,2...20）
x2 <- c(2:21) #创建一个向量
x_t <- t(x1)  #矩阵的转置，这里是向量的转置
A <- matrix(x1, nrow=4, ncol=5) #利用x1数据按列填充创建一个4×5矩阵
B <- matrix(1:20, nrow=5, ncol=4, byrow=T) #按行填充创建一个5×4矩阵，数据是1:20
A%*%B #矩阵的相乘
C<-t(B) #将B进行转置
A+C #矩阵的相加
A-C #矩阵的相减
D<-matrix(x1, 5, 5) #创建一个5阶方阵（为对称矩阵）
dim(D) #矩阵的维数
diag(D) #由矩阵的对角线元素构成的向量
diag(diag(D)) #由向量diag(A)的元素创建对角矩阵
solve(D) #矩阵的逆（solve(A,b)可解线性方程组Ax=b，b缺省时为单位矩阵）
det(D) #矩阵的行列式
eigen(D) #矩阵的特征值与特征向量
sum(diag(D)) #矩阵的迹，即对向量diag(A)中的元素求和
```
