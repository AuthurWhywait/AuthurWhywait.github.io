---
layout: post
title: "机器人学中的数学基础"
description: "机器人学中的数学基础，包括空间任意点的位置和姿态的表示、坐标和齐次坐标变换、物体的变换与逆变换、通用旋转变换以及RPY角和欧拉角"
categories: [Math]
tags: [Robotics, Matrix, Euler Angles, RPY Angles]
redirect_from:
  - /2022/02/19/
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

> 关于符号表示: $s\theta=\sin\theta, c\theta=\cos\theta$

## 1. 位置和姿态的表示

【**位置矢量**】对于直角坐标系$\{A\}$，空间任一点$p$的位置可用$3\times 1$的列矢量 $^A{p}$ 表示：

$$
^Ap=\begin{bmatrix}
    p_x\\ p_y\\ p_z
\end{bmatrix}\tag{1.1}
$$

【**旋转矩阵**】对于物体的方位（orientation），我们可由某个固接于此物体的坐标系描述。为了规定空间某刚体 $B$ 的方位，设置一直角坐标系 $\{B\}$ 与此刚体固接。用坐标系 $\{B\}$ 的三个单位主矢量 $x_B,y_B,z_B$ 相对于参考坐标系 $\{A\}$ 的方向余弦组成的 $3\times3$ 矩阵：

$$
^A_BR=\begin{bmatrix}
    ^Ax_B&^Ay_B&^Az_B
\end{bmatrix}=\begin{bmatrix}
    r_{11}&r_{12}&r_{13}\\
    r_{21}&r_{22}&r_{23}\\
    r_{31}&r_{32}&r_{33}
\end{bmatrix}\tag{1.2}
$$

来表示刚体 $B$ 相对于坐标系 $\{A\}$ 的方位，其中 $^A_BR$ 称为旋转矩阵。

> 上标 $A$ 表示代表参考坐标系 $\{A\}$ ，下标 $B$ 表示被描述的坐标系 $\{B\}$ 。其中，$^A_BR$ 的三个列矢量 $^Ax_B,^Ay_B,^Az_B$ 都是**单位矢量**且**两两垂直**。

旋转矩阵 $^A_BR$ 正交，且满足条件

$$
\begin{matrix}
    ^A_BR^{-1}={}^A_BR^{T};&\vert ^A_BR\vert =1
\end{matrix}\tag{1.3}
$$

因为其正交性质 $(1.3)$ ，我们有

$$
^B_AR={}^A_BR^{-1}={}^A_BR^{T}\tag{1.4}
$$

对于轴 $x,y,z$ 作转角为 $\theta$ 的旋转变换，其旋转矩阵分别为：

$$
\begin{matrix}
    R(x,\theta)=\begin{bmatrix}
        1&0&0\\
        0&c\theta&-s\theta\\
        0&s\theta&c\theta
    \end{bmatrix},&
    R(y,\theta)=\begin{bmatrix}
        c\theta&0&-s\theta\\
        0&1&0\\
        s\theta&0&c\theta
    \end{bmatrix},&
    R(z,\theta)=\begin{bmatrix}
        c\theta&-s\theta&0\\
        s\theta&c\theta&0\\
        0&0&1
    \end{bmatrix}
\end{matrix}\tag{1.5}
$$

【**位姿描述**】首先选取 $\{B\}$ 的坐标原点（一般选择物体 $B$ 的特征点，如质心上）。相对参考系 $\{A\}$ ，刚体 $B$ 的位姿由坐标系 $\{B\}$ 来表述（其中包括刚体 $B$ 特征点的位置矢量 $^Ap_{B_O}$ 和旋转矩阵 $^A_BR$ ），即有

$$
\{B\}=\{\begin{matrix}
    ^A_BR&^Ap_{B_O}
\end{matrix}\}
$$

【手爪坐标系】为了描述手爪的位置和姿态（位姿），规定一坐标系与手抓固结，称手爪坐标系。其 $z$ 轴设在手指接近物体的方向，称接近矢量 $a$ (approach)；$y$ 轴设在两手指的联线方向，称为方位矢量 $o$ (orientation)；$x$ 轴由右手法则确定：$n=o\times a$，$n$ 称为法向矢量（normal）。如此，手爪的方位由旋转矩阵 $R$ 所规定，即

$$
R=[n,o,a]
$$

三个单位正交矢量 $n,o,a$ 描述了手爪的姿态。而手爪的位置由位置矢量 $p$ 规定，它代表手爪坐标系的原点。因此，手爪的位姿由四个矢量 $\{n,o,a,p\}$ 来描述，记为

$$
\{T\}=\{n,o,a,p\}
$$

## 2. 坐标变换

### 坐标平移方程

$$
^Ap={}^Bp+{}^Ap_{B_O}\tag{2.1}
$$

### 坐标旋转方程

$$
^Ap={}^A_BR^Bp\tag{2.2}
$$

### 一般情况（平移和旋转的复合）

$$
^Ap={}^A_BR^Bp+{}^Ap_{B_O}\tag{2.3}
$$

## 3. 齐次坐标变换

【齐次变换形式】式子 $(2.3)$ 对于点 $^Bp$ 而言非齐次，若要齐次，做如下变形：

$$
\begin{bmatrix}
    ^Ap\\ 1
\end{bmatrix}=\begin{bmatrix}
    ^A_BR&^Ap_{B_O}\\
    0&1
\end{bmatrix}\begin{bmatrix}
    ^Bp\\ 1
\end{bmatrix}\tag{3.1}
$$

其中，$4\times 1$ 的列矢量表示三位空间的点，称为点的齐次坐标，仍然记为齐次坐标，仍然记为 $^Ap$ 或 $^Bp$。于是上式可写为矩阵形式

$$
\begin{matrix}
    ^Ap={}^A_BT^Bp,&while&^A_BT=\begin{bmatrix}
        ^A_BR&^Ap_{B_O}\\
        0&1
    \end{bmatrix}
\end{matrix}=\begin{bmatrix}
    n_x&o_x&a_x&p_x\\
    n_y&o_y&a_y&p_y\\
    n_z&o_z&a_z&p_z\\
    0&0&0&1
\end{bmatrix}\tag{3.2}
$$

空间某点 $p$ 的直角坐标描述和齐次坐标描述分别为：

$$
\begin{matrix}
    p=\begin{bmatrix}
        x\\ y\\ z
    \end{bmatrix},&p=\begin{bmatrix}
        x\\ y\\ z\\1
    \end{bmatrix}=\begin{bmatrix}
        \omega x\\\omega  y\\\omega  z\\\omega
    \end{bmatrix}
\end{matrix}
$$

其中，$\omega$为非零常数，为【**坐标比例系数**】。

坐标原点的矢量，即零矢量表示为 $[0,0,0,1]^T$。矢量 $[0,0,0,0]^T$ 没有定义。具有形如 $[a,b,c,0]$ 的矢量表示无限远矢量（无穷远点），用来表示方向，我们把包括无穷远点的空间称为扩大空间，而把第4个元素非零的点称为非无穷远点。$[1,0,0,0],[0,1,0,0],[0,0,1,0]$ 分别表示 $x,y,z$ 轴的方向。

### 点积和交积

两矢量的点积（标量）：

$$
a\cdot b=a_xb_x+a_yb_y+a_zb_z
$$

交积（矢量）：

$$
a\times b=\left\vert\begin{array}{ccc}
    i& j &k\\
    a_x& a_y &a_z\\
    b_x& b_y&b_z
\end{array}\right\vert
$$

### 平移齐次坐标系

$$
Trans(a,b,c)=\begin{bmatrix}
    1&0&0&a\\
    0&1&0&b\\
    0&0&1&c\\
    0&0&0&1\\
\end{bmatrix}
$$

非零常数乘以变换矩阵的每个元素，不改变该变换矩阵的特性。

### 旋转齐次坐标变换

改造 $(1.5)$，可以得到对应于轴 $x,y,z$ 作转角为 $\theta$ 的旋转变换，分别可得

$$
\begin{matrix}
    Rot(x,\theta)=\begin{bmatrix}
        1&0&0&0\\
        0&c\theta&-s\theta&0\\
        0&s\theta&c\theta&0\\
        0&0&0&1
    \end{bmatrix},&
    Rot(y,\theta)=\begin{bmatrix}
        c\theta&0&-s\theta&0\\
        0&1&0&0\\
        s\theta&0&c\theta&0\\
        0&0&0&1
    \end{bmatrix},&
    Rot(y,\theta)=\begin{bmatrix}
        c\theta&-s\theta&0&0\\
        s\theta&c\theta&0&0\\
        0&0&1&0\\
        0&0&0&1
    \end{bmatrix}
\end{matrix}
$$

### 变换矩阵左乘和右乘的解释

> 矩阵的乘法不具有交换性质，即 $AB\ne BA$

- 变换顺序“从右向左”，指明运动是相对固定坐标系而言；
- 变换顺序“从左向右”，指明运动是相对运动坐标系而言。

## 4. 物体的变换及逆变换

### 物体位置描述

如果我们想对一个坐标系内的多个点进行变换，我们可以将这多个点的点坐标作为列坐标组合得到一个矩阵，然后可以“快乐搞批发”。

$$
[{}^Ap_{1},{}^Ap_{2},...,{}^Ap_{n}]={}^A_BT[{}^Bp_{1},{}^Bp_{2},...,{}^Bp_{n}]\tag{4.1}
$$

### 复合变换

$$
^A_CT={}^A_BT{}^B_CT=\begin{bmatrix}
        ^A_BR&^Ap_{B_O}\\
        0&1
    \end{bmatrix}\begin{bmatrix}
        ^B_CR&^Ap_{C_O}\\
        0&1
    \end{bmatrix}=\begin{bmatrix}
        ^A_BR{}^B_CR&^A_BR^Bp_{C_O}+^Ap_{B_O}\\
        0&1
    \end{bmatrix}\tag{4.2}
$$

### 齐次变换的逆变换

方法有二，一种是直接对 $4\times 4$ 的齐次变换矩阵 $^A_BT$ 求逆；另一种是利用齐次变换矩阵的特点，简化矩阵求逆运算。

#### 正交法

对于

$$
^A_BT=\begin{bmatrix}
        ^A_BR&^Ap_{B_O}\\
        0&1
\end{bmatrix}
$$

我们有

$$
^B_AT={}^A_BT^{-1}=\begin{bmatrix}
        ^A_BR^T&-^A_BR^T{}^Ap_{B_O}\\
        0&1
\end{bmatrix}\tag{4.3}
$$

证明如下：

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/IMG_1678(20220219-194531).PNG" width="400"/></div>

#### 直接法

若

$$
T=\begin{bmatrix}
    n_x&o_x&a_x&p_x\\
    n_y&o_y&a_y&p_y\\
    n_z&o_z&a_z&p_z\\
    0&0&0&1
\end{bmatrix}
$$

则其逆变换为

$$
T^{-1}=\begin{bmatrix}
    n_x&n_y&n_z&-p\cdot n\\
    o_x&o_y&o_z&-p\cdot o\\
    a_x&a_y&a_z&-p\cdot a\\
    0&0&0&1
\end{bmatrix}\tag{4.4}
$$

## 5. 通用旋转变换

研究某个绕着从原点出发的任一矢量（轴）$f$ 旋转 $\theta$ 角时的旋转矩阵。

### 通用旋转变换公式

> 通过 $f$ 和 $\theta$ 去求旋转变换矩阵。

假设 $f$ 为坐标系 $\{C\}$ 的 $z$ 轴上的单位矢量，即

$$
C=\begin{bmatrix}
    n_x&o_x&a_x&0\\
    n_y&o_y&a_y&0\\
    n_z&o_z&a_z&0\\
    0&0&0&1
\end{bmatrix}\\
f=a_xi+a_yj+a_zk
$$

于是绕矢量 $f$ 旋转相当于绕坐标系 $\{C\}$ 的 $z$ 轴旋转，即有

$$
Rot(f,\theta)=Rot(c_z,\theta)\tag{5.1}
$$

而通过推导和化简，可以得到

$$
Rot(f,\theta)=\begin{bmatrix}
    f_xf_xvers\theta+c\theta&f_yf_xvers\theta-f_zs\theta&f_zf_xvers\theta+f_ys\theta&0\\
    f_xf_yvers\theta+f_zs\theta&f_yf_yvers\theta+c\theta&f_zf_yvers\theta-f_xs\theta&0\\
    f_xf_zvers\theta+f_zs\theta&f_yf_zvers\theta+f_xs\theta&f_zf_zvers\theta+c\theta&0\\
    0&0&0&1
\end{bmatrix}\tag{5.2}
$$

<!-- 推导和化简过程： -->

<!-- <div align=center><img src="" width=""/></div> -->

<!-- todo: -->

### 等效转角与转轴

> 通过旋转变换矩阵求解其等效的转轴与等效转角，是上一小部分的反向问题。

由任一旋转变换，能够通过式 $(5.2)$ 求得等效旋转角 $\theta$ 的转轴。

对于旋转变换：

$$
R=\begin{bmatrix}
    n_x&o_x&a_x&0\\
    n_y&o_y&a_y&0\\
    n_z&o_z&a_z&0\\
    0&0&0&1
\end{bmatrix}=\begin{bmatrix}
    f_xf_xvers\theta+c\theta&f_yf_xvers\theta-f_zs\theta&f_zf_xvers\theta+f_ys\theta&0\\
    f_xf_yvers\theta+f_zs\theta&f_yf_yvers\theta+c\theta&f_zf_yvers\theta-f_xs\theta&0\\
    f_xf_zvers\theta+f_zs\theta&f_yf_zvers\theta+f_xs\theta&f_zf_zvers\theta+c\theta&0\\
    0&0&0&1
\end{bmatrix}
$$

#### 等效转角

$$
\tan\theta=\frac{s\theta}{c\theta}=\frac{\sqrt{(o_z-a_y)^2+(a_x-n_z)^2+(n_y-o_x)^2}}{n_x+o_y+a_z-1}
$$

#### 等效转轴

$$
f=(f_x,f_y,f_z),while\begin{cases}
    f_x=(o_z-a_y)/2s\theta\\
    f_y=(a_x-n_z)/2s\theta\\
    f_z=(n_y-o_x)/2s\theta
\end{cases}
$$

## 6. 欧拉角与RPY角

### 绕固定轴 $x-y-z$ 轴旋转($RPY$角)

- Roll：绕$z$轴的旋转($\alpha$角)
- Pitch: 绕$y$轴的旋转($\beta$角)
- Yaw: 绕$x$轴的旋转($\gamma$角)

【**描述坐标系 $\{B\}$ 的法则**】$\{B\}$ 的初始方位与参考系 $\{A\}$ 重合。首先将 $\{B\}$ 绕 $z_A$ 转 $\gamma$ 角，再绕 $y_A$ 转 $\beta$ 角，最后绕 $z_A$ 转 $\alpha$ 角。

#### 求旋转矩阵

因为三次旋转都是相对于固定坐标系 $$\{A\}$$ 而言，所以按照“**从右向左**”原则，得到相应的旋转矩阵

$$
^A_BR_{xyz}(\gamma,\beta,\alpha)=R(z_A,\alpha)R(y_A,\beta)R(x_A,\gamma)\tag{6.1}
$$

最后可得

$$
^A_BR_{xyz}(\gamma,\beta,\alpha)=\begin{bmatrix}
    c\alpha~c\beta&c\alpha~s\beta~s\gamma-s\alpha~c\gamma&c\alpha~s\beta~c\gamma+s\alpha~s\gamma\\
    s\alpha~c\beta&s\alpha~s\beta~s\gamma+c\alpha~c\gamma&s\alpha~s\beta~c\gamma-c\alpha~s\gamma\\
    -s\beta&c\beta~s\gamma&c\beta~c\gamma
\end{bmatrix}\tag{6.2}
$$

#### RPY角反解

对于旋转矩阵

$$
^A_BR_{xyz}(\gamma,\beta,\alpha)=\begin{bmatrix}
    r_{11}&r_{12}&r_{13}\\
    r_{21}&r_{22}&r_{23}\\
    r_{31}&r_{32}&r_{33}
\end{bmatrix}\tag{6.3}
$$

由式 $(6.2)$ 和 $(6.3)$，我们可以求得

$$
cos\beta=\sqrt{r_{11}^2+r_{21}^2}
$$

如果 $\cos\beta\ne0$，

$$
\begin{cases}
    \beta=A\tan2(-r_{31},\sqrt{r_{11}^2+r_{21}^2})\\
    \alpha=A\tan2(r_{21}.r_{11})\\
    \gamma=A\tan2(r_{32},r_{33})
\end{cases}\tag{6.4}
$$

> 关于 $A\tan2(y,z)$ 见附录。

如果 $\beta=90^\circ$,

$$
\begin{cases}
    \beta=90^\circ\\
    \alpha=0\\
    \gamma=A\tan2(r_{12},r_{22})
\end{cases}
$$

如果 $\beta=-90^\circ$,

$$
\begin{cases}
    \beta=-90^\circ\\
    \alpha=0\\
    \gamma=-A\tan2(r_{12},r_{22})
\end{cases}
$$

### $z-y-x$ 欧拉角

【**描述坐标系 $\{B\}$ 的法则**】$\{B\}$ 的初始方位与参考系 $\{A\}$ 相同。首先使 $\{B\}$ 绕 $z_B$ 转 $\alpha$ 角，再绕 $y_B$ 转 $\beta$ 角，最后绕 $x_B$ 转 $\gamma$ 角。

这种描述方法中，**各次转动都是相对于运动坐标系的某轴进行的**，而不是相对于固定的参考系 $\{A\}$。这样的三次转动称为欧拉角，有因转动的顺序是绕$z$轴、$y$轴和$x$轴，故这种描述法为 $z-y-x$ 欧拉角。

#### 求zyx欧拉角

另外，因为“各次转动都是相对于运动坐标系的某轴进行的”，所以根据“从左向右”的原则来安排各次旋转对应的矩阵：

$$
^A_BR_{zyx}(\alpha,\beta,\gamma)=R(z,\alpha)R(y,\beta)R(x,\gamma)
$$

矩阵相乘得到

$$
^A_BR_{zyx}(\alpha,\beta,\gamma)=\begin{bmatrix}
    c\alpha~c\beta&c\alpha~s\beta~s\gamma-s\alpha~c\gamma&c\alpha~s\beta~c\gamma+s\alpha~s\gamma\\
    s\alpha~c\beta&s\alpha~s\beta~s\gamma+c\alpha~c\gamma&s\alpha~s\beta~c\gamma-c\alpha~s\gamma\\
    -s\beta&c\beta~s\gamma&c\beta~c\gamma
\end{bmatrix}\tag{6.5}
$$

#### 反解zyx欧拉角

我们可以发现式 $(6.5)$ 与式 $(6.2)$ 完全相同，故而角度 $\alpha,\beta,\gamma$ 的求解也可以使用式 $(6.4)$ 。

> 为什么相同的原因：绕固定轴旋转的顺序若与绕运动轴旋转的顺序相反，且旋转的角度也对应相等时，所得到的变换矩阵是相同的。因此，$z-y-x$ 欧拉角与固定轴 $x-y-z$ 转角描述坐标系 $\{B\}$ 是完全等价的。

### $z-y-z$欧拉角

【**描述坐标系 $\{B\}$ 的法则**】$\{B\}$ 的初始方位与参考系 $\{A\}$ 重合。首先使 $\{B\}$ 绕 $z_B$ 转 $\alpha$ 角，再绕 $y_B$ 转 $\beta$ 角，最后绕 $z_B$ 转 $\gamma$ 角。

#### 求zyz欧拉角的旋转矩阵

同样，因为转动相对于运动坐标系而言，所以使用“从左向右”原则，去求旋转矩阵：

$$
^A_BR_{zyx}(\alpha,\beta,\gamma)=R(z,\alpha)R(y,\beta)R(z,\gamma)
=\begin{bmatrix}
    c\alpha~c\beta~c\gamma-s\alpha~s\gamma&-c\alpha~s\beta~s\gamma-s\alpha~c\gamma&c\alpha~s\beta\\
    s\alpha~c\beta~c\gamma+c\alpha~s\gamma&-s\alpha~c\beta~s\gamma+c\alpha~c\gamma&s\alpha~s\beta\\
    -s\beta~c\gamma&s\beta~s\gamma&c\beta
\end{bmatrix}
$$

#### 反解zyz欧拉角

令旋转矩阵如下

$$
^A_BR_{zyz}(\alpha,\beta,\gamma)=\begin{bmatrix}
    r_{11}&r_{12}&r_{13}\\
    r_{21}&r_{22}&r_{23}\\
    r_{31}&r_{32}&r_{33}
\end{bmatrix}
$$

如果 $\sin\beta\ne0$，则

$$
\begin{cases}
    \beta=A\tan2(\sqrt{r_{31}^2+r_{32}^2},r_{33})\\
    \alpha=A\tan2(r_{23},r_{13})\\
    \gamma=A\tan2(r_{32},-r_{31})
\end{cases}
$$

如果 $\beta=0^\circ$,

$$
\begin{cases}
    \beta=0\\
    \alpha=0\\
    \gamma=A\tan2(-r_{12},r_{11})
\end{cases}
$$

如果 $\beta=180^\circ$,

$$
\begin{cases}
    \beta=180^\circ\\
    \alpha=0\\
    \gamma=A\tan2(r_{12},-r_{11})
\end{cases}
$$

## 附录

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220219221052.png"/></div>

## 参考

[1] 蔡自兴. (2000). 机器人学 (1st ed.). 清华大学出版社.

[2] 熊有伦. (1996). 机器人技术基础. 华中科技大学出版社.
