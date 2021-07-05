---
layout: post
title: "光学工程基础 清华大学（1） 绪论"
description: "光学工程基础-清华大学 学堂在线"
categories: [Optic]
tags: [Optic, THU]
redirect_from:  
  - /2021/07/05/
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

## 课程背景和内容介绍

光的基本属性：1）光是能量的载体；2）光是信息的载体。

光学：研究光的行为和性质以及光和物质相互作用的物理学科。

- 几何光学：光是携带了能量的几何线；
- 波动光学：光是电磁场的传播；
- 量子光学：光是能量粒子的辐射。
- 物理光学（含量子光学和波动光学）：专门研究光的本质属性、光的传播规律、光与物质相互作用的关系。波动光学和量子光学分别揭示了光的本质属性“波粒二象性”。
- 几何光学是波动光学在波长趋近于0时的一种近似，在光学仪器设计中较为实用。

光学工程的相关学科：信息科学、能源科学、材料科学、生命科学、空间科学、精密机械、计算机科学、微电子技术。

## 光学工程的特点

激光具有方向性好、亮度高、单色性好的特点。

全息显示是利用光的干涉与衍射原理，将激光的干涉条纹记录在材料中，可以真实地显示出物体的三维信息。

## 课程的学习方法

- 物理性质基本概念
- 实际问题模型化
- 熟能生巧

---

## 常用函数

$step$函数（阶跃函数）

$$
step(x) =
\begin{cases}
1, &x>0\\
\frac{1}{2}, &x= 0\\
0, &x<0
\end{cases}
$$

$sgn$函数（符号函数）

$$
sgn(x) =
\begin{cases}
1, &x>0\\
0, &x=0\\
-1, &x<0
\end{cases}
$$

$rect$函数（门函数）

$$
rect(\frac{x}{a})=
\begin{cases}
1, & |x|\le\frac{a}{2}\\
0, &其他
\end{cases}
$$

$tri$函数：主要在光学工程中主要表示光瞳为矩形的非相干成像系统的光学传递函数

$$
tri(\frac{x}{a})=
\begin{cases}
1-\frac{|x|}{a}, &|x|\le a\\
0,&其他
\end{cases}
$$

$sinc$函数：在光学工程的基础课程中，$sinc(x)$用来描述狭缝或矩孔的夫琅和费衍射图样。

$$
sinc(\frac{x}{a})=\frac{sin(\frac{\pi x}{a})}{\frac{\pi x}{a}}
$$

$gaus$函数：在原点有最大值1，在整个曲线下的面积为b。用来描述激光器发出的高斯光束。

$$
Gaus(x) = exp(-\pi (\frac{x}{b})^2)
$$

一些二维函数：

$$
\begin{aligned}
rect(x,y) &= rect(x)rect(y) \\
tri(x,y) &= tri(x)tri(y)\\
sinc(x,y) &= sinc(x)sinc(y)\\
gaus(x,y) &= gaus(x)gaus(y)
\end{aligned}
$$

圆域函数：常用来表示圆孔的透过率

$$
circ(\sqrt{\frac{x^2+y^2}{r_0^2}}) =
\begin{cases}
1, &\sqrt{x^2+y^2}\le r_0 \\
0, &其他  
\end{cases}
$$

贝塞尔函数：是一个二阶齐次线性偏分方程解的形式。这个方程的解主要包括n阶的第一类贝塞尔函数和n阶的第二类贝塞尔函数。本门课程中，我们主要用到的是**一阶第一类贝塞尔函数**：

$$
J_1(x) = \sum_{k=0}^\infty \frac{(-1)^k}{k!(k+1)!}(\frac{x}{2})^{2k+1}
$$

> 贝塞尔函数是圆域函数的傅里叶变换。

$Delta$函数（脉冲函数）：物理学家狄拉克用来描述极为窄小、幅值趋于无穷大的物理量。可以表示在某一点高度集中的量，这个点没有大小，但是有质量。 此外，此函数还可以看成一个连续普通函数构成的序列的极限。比如一维矩形的脉冲，这个脉冲宽度逐渐变小，幅度逐渐变大。Delta函数可以看作rect函数的极限，也可以看成gaus函数的极限，还可以看成其他普通函数的极限。

$$
\delta(x)=0,\ x\ne 0\\
\ \\
\int_{-\infin}^{\infin}\delta (x)dx = 1
$$

$Delta$函数的性质：

- 广义函数 $\iint \delta(x,y)\varphi(x,y)dxdy = \varphi(0,0)$;
- 筛选性质 $\iint \delta(x-x_0,y-y_0)\varphi(x,y)dxdy = \varphi(x_0,y_0)$;
- 比例变换性质 $\delta (ax,by) = \frac{1}{|ab|}\delta(x,y)$;
- 与普通函数的乘积 $h(x,y)\delta(x-x_0,y-y_0) = h(x_0,y_0)\delta(x-x_0,y-y_0)$.

梳状函数：是多个delta函数的组合构成。沿x轴分布、间隔为1的无穷多个脉冲函数的集合。

$$
comb(x) = \sum_{n=-\infin}^{+\infin}\delta(x-n)
$$

- 梳状函数具有**抽样能力**。
- 梳状函数的缩放性质：$\sum_{n=-\infin}^{\infin}\delta(x-n\tau) = \frac{1}{\tau}\sum_{n=-\infin}^{\infin}\delta(\frac{x}{\tau}-n) = \frac{1}{\tau}comb(\frac{x}{\tau})$

## 常用函数的运算与变换

### 卷积

卷积的定义（其中$*$表示**卷积运算**）：

$$
\begin{aligned}
g(x,y) &= \iint_{-\infin}^{\infin}f(\xi, \eta)h(x-\xi,y-\eta)d\xi d\eta\\
&= f(x,y)*h(x,y)
\end{aligned}
$$

卷积具有**展宽、平滑**的效果，并且满足**交换律**、**结合律**、**分配律**和**平移不变性**。

$$
\begin{aligned}
f(x) * h(x) &= h(x) * f(x)\\
[f(x)*g(x)]*h(x)&=f(x)*[g(x)*h(x)]\\
[a\cdot f(x)+b\cdot g(x)]*h(x) &= a\cdot [f(x)*h(x)] + b\cdot [f(x)*h(x)]\\
g(x-x_0) &= f(x) * h(x-x_0)
\end{aligned}
$$

### 相关

相关的定义（$\star$表示相关运算）：反应两个函数的相似程度。

$$
f(x)\star g(x) =
\iint_{-\infin}f(\xi,\eta)g^*(\xi-x,\eta-y)d\xi d\eta
$$

相关可以用卷积的形式来表示：

$$
\begin{aligned}
    f(x)\star g(x) &= \int_{-\infin}^{\infin}f(\xi)g^*(\xi-x)d\xi\\
    &=\int_{-\infin}^{\infin}f(\xi)g^*\frac{x-\xi}{-1}d\xi\\
    &=f(x)*g^*(-x)
\end{aligned}
$$

## 空间域的傅里叶变换

一幅图像同样存在高频、中频和低频的情况。一副图像的特征，可以用它的频谱来表示，所有的频率成分和相应的振幅系数，就是这幅图像所包含的全部信息。

- 空间周期：$T_x=d_x,\ T_y=d_y$
- 空间频率：$f_x=1/d_x,\ f_y=1/d_y$

二维傅里叶变换的定义：

$$
\begin{aligned}
g(x,y) &= \iint_{-\infin}G(f_x,f_y)exp[j2\pi(f_xx+f_yy)]df_xdf_y\\
G(f_x,f_y)&=\iint_{-\infin}g(x,y)exp[-j2\pi(f_xx+f_yy)]dxdy
\end{aligned}
$$

> $g(x,y)$是$G(x,y)$的傅里叶变换；而$G(x,y)$是$g(x,y)$的傅里叶变换。$g(x,y)$的坐标是空间坐标，而$G(x,y)$的坐标是空间频率坐标。其中$exp[j2\pi(f_xx+f_yy)]$以及$exp[-j2\pi(f_xx+f_yy)]$为核函数。

sinc函数是rect函数的傅里叶变换（即rect函数是sinc函数的逆傅里叶变换）。

$$
\begin{aligned}
    \mathscr{F}\{rect(x)\} &= \int_{-\frac{1}{2}}^{\frac{1}{2}}e^{-j2\pi f_x}dx\\
    &=\frac{1}{j2\pi f}(e^{j\pi f}-e^{-j\pi f})\\
    &=\frac{sin \pi f}{\pi f}\\
    &=sinc(f_x)
\end{aligned}
$$

【傅里叶变换的位移定理】空域中的位移会带来频域中的相移，同样，频域中的位移，会带来空域中的相移。

$$
\mathscr{F}\{g(x-a,y-b)\}=G(f_x,f_y)exp[-j2\pi(af_x+bf_y)]\\
\ \\
\mathscr{F}\{g(x,y)exp[j2\pi(xf_x+yf_y)]\}=G(f_x-f_a,f_y-f_b)
$$

【傅里叶变换的卷积定理】复杂函数可以表示为简单函数乘积或者是卷积时，利用卷积定理，就可以由简单函数的变化式来确定复杂函数的变换式。（给我们求一个函数的卷积提供了途径）

$$
\mathscr{F}\{g(x,y)*h(x,y)\}=G(f_x,f_y)\cdot H(f_x,f_y)\\
\mathscr{F}\{g(x,y)\cdot h(x,y)\}=G(f_x,f_y)*H(f_x,f_y)
$$

【两次傅里叶变换】会使得函数的自变量符号相反。

$$
\mathscr{FF}\{g(x,y)\}=\mathscr{F}\{G(f_x,f_y)\}=g(-x,-y)
$$

【圆域函数的傅里叶变换是贝塞尔函数】

$$
\begin{aligned}
    B\{circ(r)\}&=\frac{1}{2\pi \rho^2}\int_0^{2\pi \rho}r'J_0(r')dr'\\
    &=\frac{J_1(2\pi \rho)}{\rho}
\end{aligned}
$$
