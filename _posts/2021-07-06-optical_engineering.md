---
layout: post
title: "《光学工程基础》清华大学（2）- 应用光学（光波、光线和成像）"
description: "光学工程基础-清华大学 学堂在线"
categories: [Optic]
tags: [Optic, THU]
redirect_from:  
  - /2021/07/06/
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

## 基本概念和光线传播基本定律

光是电磁波的一种，覆盖特定的波长范围。

光波指的是波长在0.1微米到30微米左右的这个波段，包括紫外、可见、近红外、中红外、远红外等波段。可见光波主要包括400纳米~760纳米的波段。

真空中光的传播速度是一个恒定值：c = 299792458 m/s。

> 国际单位中**米**的定义就是根据光的传播速度而来的。

光波的速度$v$、波长$\lambda$和频率$\nu$:

$$
v = \lambda \nu
$$

> 注意区别$v$和$\nu$。

折射率：

$$
n=c/v=n*(\lambda)
$$

> 折射率是一个比值，与波长相关，体现出色散行为。

【光源】从物理学的观点看，任何发光的物体都可以叫作**光源**。在应用光学中，把凡是发出光线的物体，**不论它本身发出光线或是因为被照明而发出光线**，都称为光源。

【发光点】如果某光源可看成几何学上的点，它只占用空间位置而无体积和线度，则称之为发光点或点光源。

【光线】光线是表示光能传播方向的几何线。

【光束】有一定关系的一些光线的集合。

【光波波面】光是一种电磁波。某一时刻其振动相位相同的点所构成的面称光波波面。在各向同性介质中，光沿光波波面法线方向传播，可以认为光波波面的发现就是应用光学中的光线，与波面对应的法线束就是光束。

【光线模型】如果光波波长与光学系统口径相比小到可以忽略，则可以抽象出应用光学中广泛使用的**光线模型**。

应用光学近似：$\textcolor{red}{\lambda=0}$
衍射方程：$dsin\theta=m\lambda$

$$
\lambda=0 \rightarrow\theta=0\rightarrow\textcolor{red}{光沿原方向传播}
$$

【光线传播基本定律】

- **直线传播**：光在均匀介质中沿直线传播。
- **独立传播**：光线以不同方向通过某点时，彼此互不影响，各光线独立传播。
- **反射定律**：1）入射光线、法线和反射光线在同一平面内；2）入射光线和反射光线在法线的两侧；3）反射角等于入射角 $I'=-I$。
- **折射定律**：1）入射光线、法线和折射光线在同一平面内；2）入射光线和折射光线在法线的两侧；3）入射角与折射角的正弦之比与入射角无关，是一个与介值与光的波长有关的常数：$n'sinI'=nsinI$
- **全反射**：1）当光从光密介质（$n$大）入射向光疏介质（$n'$小）且入射角$I$增大到某一程度时，折射角$I'$达到90°，折射光线沿界面掠射出去，此时的入射角度称为临界角，记为$I_c$。2）若入射角继续增大，入射角$I$大于临界角$I_c$的光线不能折射进入第二种介质，而全部反射回第一种介质，即发生了全反射。
- **光路可逆**：光线传播方向可逆。

> 反射定律和折射定律统称为：<font color="red">斯涅尔（Snell）定律</font>。在$n'=-n$时，折射定律可推导出反射定律。

## 成像基本概念

【像】：从物体发出的光线经平面镜、球面镜、透镜、棱镜等反射或折射后所形成的与原物相似的图景。分为实像和虚像。

成像三种说法：波面、光线、等光程。

【波面】以及【光线】定义见上文

【光程】路程与相应折射率乘积之和称为光从$P$到$P'$的光程：

$$
\begin{aligned}
    [PP']&=\sum_{i=1}^mn_il_i\\
    &or\\
    [PP']&=\int_P^{P'}ndl\ (若折射率连续变化)
\end{aligned}
$$

> 光程就是**光在介质中走过一段几何路程所需的时间内**<font color="red">光在真空中所走的路程</font>，简言之，光程是等效真空程。

点物成点像就是物点与像点之间的光程无论沿哪条实际路径都相等。（由**费马原理**导出）

> 物点和像点之间连续分布着无穷多条实际的路径。根据**费马原理**，它们的光程都应该取极值，这些连续分布的实际路径的光程都取极大值或极小值是不可能的，**唯一的可能是取恒定值**，即它们的**光程相等**。
>
> （费马原理见下面章节）

## 费马原理

费马原理在应用光学是非常重要的一个原理，特别是在求解复杂光学系统的时候，我们可以通过费马原理，来得到解或者初始解。

【费马(Fermat)原理】光从空间一点传播到另一点是沿着**光程为极值**的路径传播的。

> 具体地说，把光传播的实际路径与其邻近的其他路径相比较，光的实际路径的光程为**极小**、**极大**或**稳定值**。
>
> 特殊情况；**鞍点**等

$$
[PP']=\int_P^{P'}ndl\ 的一阶变分等于0，即\\
\delta\int_P^{P'}ndl=0
$$

光路可逆：若光线在空间中沿某一路径传播，当光线反向时，必沿同一路径逆向传播。

【使用费马定理导出折射定律】

$$
\begin{aligned}
    PE&=\sqrt{(x_0-x)^2+(y_0-y)^2+(z_0-z)^2}=d\\
    P'E&=\sqrt{(x_0-x')^2+(y_0-y')^2+(z_0-z')^2}=d'
\end{aligned}
$$

$$
\underset{P-E-P'}{[PP']}=nd+n'd',\ (P-E-P')
$$

下面研究$PGP'$（用矢量以及矢量的点积来表示）

$$
\underset{P-G-P'}{[PP']}=n\sqrt{(d\mathbf{a}+\mathbf{\delta})\cdot(d\mathbf{a}+\mathbf{\delta})}+n'\sqrt{(d'\mathbf{a'}-\mathbf{\delta})\cdot(d'\mathbf{a'}-\mathbf{\delta})}
$$

求解两个光程的光程差：

$$
\begin{aligned}
    \Delta[PP']=&\underset{P-G-P'}{[PP']}-\underset{P-E-P'}{[PP']}\\
    =&n\sqrt{d^2\mathbf{a}\cdot\mathbf{a}+2d\mathbf{a}\cdot\mathbf{\delta}+\mathbf{\delta}\cdot\mathbf{\delta}}-nd\\
    &+n'\sqrt{d'^2\mathbf{a'}\cdot\mathbf{a'}+2d'\mathbf{a'}\cdot\mathbf{\delta}+\mathbf{\delta}\cdot\mathbf{\delta}}-n'd'
\end{aligned}
$$

使用Taylor级数展开：$when\ x<<1,\ \sqrt{1+x}\approx 1+\frac{1}{2}x$，带入，得

$$
\begin{aligned}
    \Delta[PP']=&\underset{P-G-P'}{[PP']}-\underset{P-E-P'}{[PP']}\\
    =&nd(1+\frac{\mathbf{a\cdot\delta}}{d})-nd+n'd'(1-\frac{\mathbf{a'\cdot\delta}}{d})-n'd'\\
    =&(n\mathbf{a}-n'\mathbf{a'})\cdot\delta
\end{aligned}
$$

根据费马原理，对任意$\delta$，$\Delta[PP']$具有相同的正负号，而根据$\delta$方向的任意性，可知：

$$
(n\mathbf{a}-n'\mathbf{a'})\cdot\delta=0
$$

在$\delta$很小的时候，$\delta$的方向近似于切线方向，故而$(n\mathbf{a}-n'\mathbf{a'})$的分量只在法向上有分量。

$$
\begin{aligned}
    (n\mathbf{a}-n'\mathbf{a'})\cdot\delta&=0\\
    n'\mathbf{a'}-n\mathbf{a}&=\Gamma N\\
    n\mathbf{a}\times N&=n'\mathbf{a'}\times N
\end{aligned}
$$

化简得

$$
n'sinI'=nsinI\ \ \ (折射定律)
$$

## 等光程成像

物点和像点之间连续分布着无穷多条实际的光线路径。根据费马原理，它们的光程都应取极值，这些连续分布的时间光线的光程都去极大值或极小值是不可能的，唯一的可能是取极值，即它们的光程相等。

【**马吕斯定律**】垂直于波面的光线束（法线集合）经过任意多次反射和折射后，无论折射面和反射面形状如何，出射光束仍为法线集合的性质。并且入射波面与出射波面对应点之间的光程均为定值。

光线束在各向同性介质的传播过程中，始终保持着与波面的正交性。

$$
\left.\begin{matrix}
 费马原理\\
 折反射定律\\
 马吕斯定律
\end{matrix}\right\}等价
$$

> 在实际问题中，通过使用两条路径光程相等解题。

## 常用曲面形状

广义地说，光学系统是由若干几何曲面串连在一起构成的，这些曲面就是两种介质的分界面。

常用的曲面形状：

- 球面
- 二次回转抛物面
- 二次回转椭球面
- 二次回转双曲面

【共轴光学系统】通常在串连这些曲面时，将各个球面的**球心**，以及二次回转曲面的**回转轴**都放在光学系统的集合对称轴上，该对称轴为光学系统的光轴，这一类光学系统称为共轴光学系统。

【<font color='red'>球面</font>】

$$
r^2=x^2+y^2+(z-r)^2\\
令h^2=x^2+y^2,\\
则z^2=2zr+h^2=0\\
解得：z=r\pm\sqrt{r^2-h^2}\\
\textcolor{red}{通常情况下只关注第一个交点}，即z=r-\sqrt{r^2-h^2}
$$

此外，在应用光学中，我们通常把半径提出来，将其倒数记为**球面曲率**

$$
c=\frac{1}{r}\\
$$

使用泰勒展式对$z$进行化简：

$$
\begin{aligned}
    z&=r[1-\sqrt{1-(\frac{h}{r})^2}]\\
    &=\frac{1-\sqrt{1-(ch)^2}}{c}\\
    &=\frac{ch^2}{1+\sqrt{1-(ch)^2}}\\
    &=\frac{1}{2}ch^2+\frac{1}{8}c^3h^4+\frac{1}{16}c^5h^6+...
\end{aligned}
$$

【<font color='red'>二次回转曲面</font>】（以椭球面为例）

$$
\frac{(z-a)^2}{a^2}+\frac{h^2}{b^2}=1
$$

同样将顶点的曲率用c来表示（$a$为椭球的长轴，$b$为椭球的短轴）：

$$
c=\frac{a}{b^2}
$$

$$
\epsilon = \frac{b^2}{a^2}
$$

则$z$可以表示为

$$
z=\frac{ch^2}{1+\sqrt{1-\epsilon(ch)^2}}
$$

在许多商用光学设计程序中，常使用下式表示二次回转曲面（其中$k$为**圆锥常数**）

$$
\begin{aligned}
    z&=\frac{ch^2}{1+\sqrt{1-(1+k)c^2h^2}}\\
    &\overset{Taylor}{=}\frac{1}{2}ch^2+\frac{1}{8}(1+k)c^3h^4+\frac{1}{16}(1+k)^2c^5h^6
\end{aligned}
$$

$$
k=\epsilon-1=\frac{b^2}{a^2}-1=-e^2
$$

> $e$ 为椭球偏心率，有的时候也叫做离心率

|       |  k>0   | $\epsilon >1$  | 扁椭球 |
| :---: | :----: | :------------: | :----: |
|  e=0  |  k=0   |  $\epsilon$=1  |   球   |
| 0<e<1 | -1<k<0 | 0<$\epsilon$<1 | 长椭球 |
|  e=1  |  k=-1  |  $\epsilon$=0  | 抛物面 |
|  e>1  |  k<-1  |  $\epsilon$<0  | 双曲面 |

【<font color='red'>轴对称高次非球面</font>】(在二次回转曲面的基础中加上一些<font color='red'项></font>)

$$
z=\frac{ch^2}{1+\sqrt{1-\epsilon(ch)^2}}+\textcolor{red}{a_4h^4+a_6h^6+a_8h^8+...}
$$

【<font color='red'>自由曲面</font>】

- 非对称
- 不规则
- 不适合用同一的数学方程式描述
- 微米级或亚微米级面形精度和纳米量级粗糙度

> 自由曲面在实际生活中的应用越来越多。
