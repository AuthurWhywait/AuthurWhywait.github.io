---
layout: post
title: "深度学习优化器"
description: "Brief introduction of Optimizers in Deep Learning"
categories: [DeepLearning]
tags: [Optimizer]
redirect_from:
  - /2022/06/17/
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
    <link rel="stylesheet" href="//unpkg.com/gitalk/dist/gitalk.css">
    <script src="//unpkg.com/gitalk/dist/gitalk.min.js"></script>
    <script>
        var gitalk = new Gitalk({
            clientID: 'c5997a4ef68d75e658c7',
            clientSecret: '77b8fd83267599e9f0eae497ba480d50764142c0',
            repo: 'blog-comments',
            owner: 'AuthurWhywait',
            admin: ['AuthurWhywait'],
            // title: location.hash.match(/#(.*?)([?]|$)/)[1],
            // id: location.hash.match(/#(.*?)([?]|$)/)[1],
            id: "20220617",
        })
        // 监听URL中hash的变化，如果发现换了一个MD文件，那么刷新页面，解决整个网站使用一个gitalk评论issues的问题。
        window.onhashchange = function (event) {
            if (event.newURL.split('?')[0] !== event.oldURL.split('?')[0]) {
                location.reload()
            }
        }
        gitalk.render('gitalk-container')
    </script>
</head>

- Content
{:toc}

## 梯度下降算法（Gradient Decent, GD）

梯度下降是迭代法的一种。梯度下降法的计算过程就是沿梯度下降的方向求解极小值，当然也可以沿梯度上升方向求解最大值。

假设

- 模型参数为 $\theta$；
- 损失函数为 $J(\theta)$；
- 梯度 $\bigtriangledown_\theta J(\theta)$ 为损失函数 $J(\theta)$ 关于参数 $\theta$ 的偏导数；
- 学习率为 $\alpha$

则使用梯度下降算法更新参数为

$$
\theta_{t+1} = \theta_t - \alpha\cdot\bigtriangledown_\theta J(\theta)
$$

梯度下降算法的两个缺点：

1. <font color="blue">训练速度慢。</font>每走一步都要计算调整下一步的方向，下山的速度变慢。在应用于大型数据集中，每输入一个样本都要更新一次参数，且每次迭代都要遍历所有的样本。会使得训练过程极其缓慢，需要花费很长时间才能得到收敛解。
2. <font color="blue">容易陷入局部最优解。</font>由于是在有限视距内寻找下山的反向。当陷入平坦的洼地，会误以为到达了山地的最低点，从而不会继续往下走。所谓的局部最优解就是鞍点，到达鞍点后模型参数不再继续更新。

### 批量梯度下降算法（Batch Gradient Descent, BGD）

- 训练总样本数为$n$
- 样本为 $\{(x^1,y^1),...,(x^n,y^n)\}$
- 在第$i$对样本上$\{(x^i,y^i)\}$上损失函数关于参数的梯度为$\bigtriangledown_\theta J_i(\theta,x^i,y^i)$

则使用BGD更新参数为

$$
\theta_{t+1}=\theta_t-\alpha_t\cdot\sum_{i=1}^n\bigtriangledown_\theta J_i(\theta,x^i,y^i)
$$

> 每进行一次参数更新，需要计算整个数据样本集，因此导致批量梯度下降法的速度会比较慢，尤其是数据集非常大的情况下，收敛速度就会非常慢，但是由于**每次的下降方向为总体平均梯度，它得到的会是一个全局最优解**。批量梯度下降法**比标准梯度下降法训练时间短**，且**每次下降的方向都很正确**。

### 随机梯度下降算法（Stochastic Gradient Descent, SGB）

和BGD不同，每次参数更新只需选择一个样本 $(x^i,y^i)$ 计算其梯度，参数更新公式如下：

$$
\theta_{t+1}=\theta_t-\alpha\cdot\bigtriangledown_\theta J_i(\theta,x^i,y^i)
$$

> BGD和SGD是两个极端，SGD由于每次参数更新仅仅需要计算一个样本的梯度，**训练速度很快**，即使在样本量很大的情况下，可能只需要其中一部分样本就能迭代到最优解，由于每次迭代并不是都向着整体最优化方向，导致**梯度下降的波动非常大，更容易从一个局部最优跳到另一个局部最优**，准确度下降。

SGB缺点：

- 选择合适的learning rate比较困难 ，学习率太低会收敛缓慢，学习率过高会使收敛时的波动过大
- 所有参数都是用同样的learning rate
- SGD容易收敛到局部最优，并且在某些情况下可能被困在鞍点

### 小批量梯度下降法（mini-Batch Gradient Descent, mini-BGD）

BGD 和 SGD 是两个极端，而 mini-BGD 作为 BGD 和 SGD 的折中。对于含有n个训练样本的数据集，每次参数更新时选择一个大小为 m（m < n）的 mini-batch 数据样本计算其梯度，其参数更新公式如下：

$$
\theta_{t+1}=\theta_t-\alpha\cdot\sum_{i=x}^{i=x+m-1}\bigtriangledown_\theta J_i(\theta,x^i,y^i)
$$

小批量梯度下降法即保证了训练的速度，又能保证最后收敛的准确率，目前的SGD默认是小批量梯度下降算法。

> 1）应用大型数据集时，训练速度很快。2）mini-BGD在选择小批量样本时，同时会引入噪声，使得权值更新的方向不一定正确。3）而对于引入噪声，大量的理论和实践工作证明，只要噪声不是特别大，都能很好地收敛。

## 动量优化法（Momentum）

【思想的物理抽象】当我们将一个小球从山上滚下来，没有阻力时，它的动量会越来越大，但是如果遇到了阻力，速度就会变小。

【算法的思想】参数更新时在一定程度上保留之前更新的方向，同时又利用当前batch的梯度微调最终的更新方向，简言之就是通过积累之前的动量 $g_{sum, previous}$ 来加速当前的梯度。梯度方向在不变的维度上，参数更新变快，梯度有所改变时，更新参数变慢，这样就能够加快收敛并且减少动荡。

- gradient 表示时刻 t 时刻的动量（也就是t时刻的梯度）；
- u 表示动量因子，通常取值为 0.9 或者近似值；

我们可以在 SGD 的基础上增加动量，参数更新公式如下

$$
\begin{aligned}
    g_{sum} &= u\cdot g + g_{sum,previous}\cdot r_{decay}\\
    \delta &= - r \cdot g_{sum}\\
    \theta &= \theta + \delta
\end{aligned}
$$

- $g$: gradient
- $g_{sum}$: sum of gradient
- $g_{sum,previous}$: previous sum of gradient
- $r$: learning rate
- $r_{decay}$: decay rate

> 在梯度方向改变时，momentum能够降低参数更新速度，从而减少震荡；在梯度方向相同时，momentum可以加速参数更新， 从而加速收敛。总而言之，momentum能够**加速SGD收敛，抑制震荡。**
> 动量**移动得更快**(因为它积累的所有动量)；动量**有机会逃脱局部极小值**(因为动量可能推动它脱离局部极小值)。同样，它也将**更好地通过高原区**。

## 自适应学习率优化算法

基于小批量训练数据的**自适应学习率**算法主要有：

- AdaGrad
- RMSProp
- Adam
- lazydam

### AdaGrad（Adaptive Gradient）

【思想】独立地适应所有模型参数的学习率，每个参数以**反比于其所有梯度历史平均值总和的平方根**规则缩放，详细情况可以看下文代码的具体流程。

> 括号内为建议默认值。

- 全局学习率 $\sigma$
- 初始化参数 $\omega$
- 为了数值稳定而创建的小常数 $\delta(=10x^{-7})$
- 梯度累计变量 $r(=0)$

#### AdaGrad 算法主体

<font color="red">

1）取出小批量数据 $\{x_1,x_2,...,x_m\}$，数据对应的目标用$y_i$来表示；
2）在小批量数据的基础上按照公式计算梯度：

$$
g\leftarrow\frac{1}{m}\bigtriangledown_w\sum_iL(f(x_i;\omega),y_i)
$$

3）累积平方梯度，并刷新 $r$：

$$
r\leftarrow r+g\odot g
$$

4）计算参数更新量（ $\frac{\sigma}{\delta+\sqrt{r}}$ 会被逐元素应用）：

$$
\Delta\omega = \frac{\sigma}{\delta+\sqrt{r}}\odot g
$$

5）根据 $\Delta\omega$ 更新参数：

$$
\omega\leftarrow\omega+\Delta\omega
$$

</font>

【Adagrad 解决问题的思路】更新的特征（幅度）越多，将来要更新的就越少，这样就有机会让其他特征（例如**稀疏特征**）赶上来。特征更新幅度的衡量标准使用梯度平方的累计和表示（可视化而言就是更新这个特征的程度在这个维度中移动了多少）。

这个思路让 AdaGrad 可以**更好地避开鞍点**。

> Adagrad 将采取直线路径，而梯度下降（或者Momentum）方法“先滑下陡峭的斜坡之后才可能担心较慢的方向”。此时，梯度下降方法很有可能非常满足地停留在鞍点，因为那里两个方向的梯度都是零。

#### AdaGrad 小结

【适用范围】对出现比较多的类别数据，Adagrad 给予越来越小的学习率，而对于比较少的类别数据，会给予较大的学习率。因此 Adagrad 适用于数据稀疏或者分布不平衡的数据集。

【优势】不需要人为地调节学习率。

【缺点】随着迭代次数的增多，学习率会越来越小，最终趋于零。

### RMSprop（root mean square prop）

基于 AdaGrad 算法的基础上修改得到。AdaGrad中，每个参数的 $\Delta\omega$ 都反比于**其所有梯度历史平方值之和的平方根**，但 RMSprop 算法采用了**指数衰减平均的方式** 淡化遥远过去的历史对当前步骤参数更新量 $\Delta\omega$ 的影响。

**引入了新参数 $\rho$ 为 decay rate，用于控制历史梯度的衰减速率**。

#### RMSprop 算法主体

<font color="red">

1）取出小批量数据 $\{x_1,x_2,...,x_m\}$，数据对应的目标用$y_i$来表示；
2）在小批量数据的基础上按照公式计算梯度：

$$
g\leftarrow\frac{1}{m}\bigtriangledown_w\sum_iL(f(x_i;\omega),y_i)
$$

<font color="purple">

3）累积平方梯度（此处梯度的平方和实际为**梯度平方的衰减和**），并刷新 $r$：

$$
r\leftarrow\rho\cdot r+(1-\rho)\cdot g\odot g
$$

</font>

4）计算参数更新量（ $\frac{\sigma}{\delta+\sqrt{r}}$ 会被逐元素应用）：

$$
\Delta\omega = \frac{\sigma}{\delta+\sqrt{r}}\odot g
$$

5）根据 $\Delta\omega$ 更新参数：

$$
\omega\leftarrow\omega+\Delta\omega
$$

</font>

除了衰减之外，decay rate $\rho$ 还有一个**放缩效应**。它以一个因子 $(1-\rho)$ 的效率向下缩小整个项。换句话说，如果$\rho=0.99$，除了衰减之外，梯度的平方和约为$\sqrt{1-\rho}=0.1$，因此对于相同的学习率而言，在新梯度 $g$ 方向上迈出的那一步（可以看成是在 $g$ 方向上的投影？）会将近原来的10倍。

### Adam (Adaptive Moment Estimation)

同时兼顾了 momentum 和 RMSprop 的优点。

#### Adam 算法主体

- 全局学习率为 $\sigma(=0.001)$
- 矩估计的指数衰减速率 $\rho_1(=0.9),\rho_2(=0.99)\in[0,1)$
- 为了数值稳定而创建的小常数 $\delta(=10x^{-8})$
- 一阶、二阶矩变量$s,r(=0,0)$
- 时间计步器 $t(=0)$

<font color="red">

1）取出小批量数据 $\{x_1,x_2,...,x_m\}$，数据对应的目标用$y_i$来表示；
2）在小批量数据的基础上按照公式计算梯度：

$$
g\leftarrow\frac{1}{m}\bigtriangledown_w\sum_iL(f(x_i;\omega),y_i)
$$

3）刷新时间步：

$$
t\leftarrow t+1
$$

<font color="purple">

4）分别更新一阶、二阶有偏矩估计：

$$
s\leftarrow\rho_1\cdot s+(1-\rho_1)\cdot g\\
r\leftarrow\rho_2\cdot r+(1-\rho_2)\cdot g\odot g
$$

5）分别对一阶矩阵和二阶矩阵的偏差进行修正：

$$
\tilde{s}\leftarrow\frac{s}{1-\rho_1^t}\\
\tilde{r}\leftarrow\frac{r}{1-\rho_2^t}
$$

6）计算参数的更新量

$$
\Delta\omega = -\sigma\frac{\tilde{s}}{\sqrt{\tilde{r}+\delta}}
$$

</font>

7）根据 $\Delta\omega$ 更新参数：

$$
\omega\leftarrow\omega+\Delta\omega
$$

</font>

除了像 Adadelta 和 RMSprop 一样存储了过去梯度的平方 $r$ 的**指数衰减平均值**，也像 momentum 一样保持了过去梯度 $s$ 的**指数衰减平均值**，详情见上述代码 Step4。

> 【说明】名称为“指数衰减平均值”的一些说明。因为每一个都配一个权重$\rho$，在“历史”中存在了 $\Delta t$ 的梯度平方就相当于配上了 $\rho^{\Delta t}$，这和指数函数的的定义呼应上了。详情可以见[EMA](https://en.wikipedia.org/wiki/Moving_average)。

因为 $s$ 和 $r$ 被初始化为 0 向量，那它们就会向 0 偏置，所以做了偏差校正，通过计算偏差校正后的 $s$ 和 $r$ 来抵消这些偏差，详情见上述代码流程的 Step5。

> 【说明】分母小于零，有放大作用，相当于远离 0。随着 $t$ 的增加，$\beta^t$越来越接近0，该偏差修正对数据前期影响大，后期影响逐渐减小。

#### Adam 小结

- Adam梯度经过偏置校正后，每一次迭代学习率都有一个固定范围，使得参数比较平稳。
- 结合了Adagrad善于**处理稀疏梯度**和RMSprop善于**处理非平稳目标**的优点
- 为不同的参数计算不同的自适应学习率
- **适用于大多非凸优化问题**——适用于**大数据集**和**高维空间**。

### LazyAdam

LazyAdam 是 Adam 优化器的一种变体，可以更高效地处理稀疏更新。原始的 Adam 算法为每个可训练变量维护两个**移动平均累加器**，这些累加器在每一步都会更新。而**此类为稀疏变量提供了更加懒惰的梯度更新处理。它<font color="red">仅更新当前批次中出现的稀疏变量索引的移动平均累加器</font>，而不是更新所有索引的累加器**。与原始的 Adam 优化器相比，它可以大幅提高某些应用的模型训练吞吐量。但是，它的语义与原始的 Adam 算法略有不同，这可能会产生不同的实验结果。

---

## 参考

- [机器学习优化器Optimizer的总结](https://zhuanlan.zhihu.com/p/150113660)
- [深度学习——优化器算法Optimizer详解（BGD、SGD、MBGD、Momentum、NAG、Adagrad、Adadelta、RMSprop、Adam）](https://www.cnblogs.com/guoyaohua/p/8542554.html)

<div id="gitalk-container"></div>
