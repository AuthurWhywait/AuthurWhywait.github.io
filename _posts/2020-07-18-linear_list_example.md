---
layout: post
title: "一元多项式的表示及相加"
description: "An using example of Linear List"
categories: [Data_Structure]
tags: [Example, Linear List]
redirect_from:
  - /2020/07/18/
---

假设![Q_m(x)][Q_m(x)]是一元m次多项式，同样可用线性表Q来表示:

![线性表Q][线性表Q]

不失一般性，设另有一多项式![P_n(x)][P_n(x)]，且`m`小于`n`，则两个多项式相加的结果![R_n(x)][R_n(x)]为:![R][R].

于是，我们可以对`P`,`Q`,`R`采用顺序存储结构，使得多项式相加的算法定义十分简洁。

但是，在通常应用中，多项式的次数可能很高且变化很大，比如![S(x)][S(x)]，需要一长度为20001的线性表来表示，表中仅有3个非零元素，对于此情况，会造成空间的浪费，但是如果只存储非零系数项则显然必须同时存储相应指数。

一般情况下的一元n次多项式![一元n次多项式][一元n次多项式]，其中qi是指数为ei的项的非零系数，且满足![ei关系][ei关系]便使用

![第二种表示][第二种表示]

可确定唯一多项式![P_n(x)][P_n(x)]. 

在最坏情况下，`n+1(=m)`个系数都不为零，则比只存储每项系数的方案要多存储一倍的数据。但是对于`S(x)`类的多项式，这种表示大大节省空间。

## 存储结构

对于线性表的两种存储结构，两种表示方法也可以有两种存储结构方法。

在实际的应用程序中取哪一种，则要视多项式做何种运算而定：

如果只对多项式进行 **“求值”**等**不改变多项式的系数和指数**的运算，则采用类似顺序表的顺序存储结构即可，否则应采用链式存储表示。

>个人理解：如果存在改变多项式的系数和指数的运算，则涉及线性表的元素的插入(零变非零)和删除(非零变零)操作，如果插入和删除操作较多，则更适合链式存储表示。

## 相加

“和多项式”链表中的结点无需另生成，而应该从来嗯个多项式的链表中摘取。运算规则如下：

假设指针`qa`和`qb`分别指向多项式A和多项式B中当前进行比较的某个结点，则比较两个结点中的指数项，有下面三种情况：

1. 指针`qa`所指结点的指数值**小于**指针`qb`所指结点的指数值，则**摘取**`qa`所指结点插入到“和多项式”链表中；
2. 指针`qa`所指结点的指数值**大于**指针`qb`所指结点的指数值，则**摘取**`qb`所指结点插入到“和多项式”链表中；
3. 指针`qa`所指结点的指数值**等于**指针`qb`所指结点的指数值，则将两个结点中的系数相加，若和数不为零，则修改`qa`所指结点的系数值，同时**释放**`qb`所指结点；反之，从多项式A的链表删除相应结点，并**释放**指数`qa`和`qb`所指结点。

## 相乘

两个一元多项式相乘的算法，可以利用两个一元多项式相加的算法来实现。(因为乘法元算可以分解为一系列的加法运算)

假设`A(x)`和`B(x)`相乘，则计算`M(x)`:

![相乘][相乘]

其中，每一项都是一个一元多项式。

[Q_m(x)]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520Q_m%2528x%2529&dl=0
[线性表Q]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520Q%253D%2528q_0%252C%2520q_1%252C%2520q_2%252C...%252C%2520q_n%2529&dl=0
[P_n(x)]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520P%253D%2528p_0%252C%2520p_1%252C%2520p_2%252C...%252C%2520p_n%2529&dl=0
[R_n(x)]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520R_n%2528x%2529%253DP_n%2528x%2529%26plus%3BQ_m%2528x%2529&dl=0
[R]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520R%253D%2528p_0%26plus%3Bq_0%252C%2520p_1%26plus%3Bq_1%252C%2520p_2%26plus%3Bq_2%252C...%252Cp_m%26plus%3Bq_m%252Cp_%257Bm%26plus%3B1%257D%252C...%2520p_n%2529&dl=0
[S(x)]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520S%2528x%2529%253D1%26plus%3B3x%255E%257B10000%257D%26plus%3B2x%255E%257B20000%257D&dl=0
[一元n次多项式]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520P_n%2528x%2529%253Dp_1x%255E%257Be_1%257D%26plus%3Bp_2x%255E%257Be_2%257D%26plus%3B..%26plus%3Bp_mx%255E%257Be_m%257D&dl=0
[ei关系]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%25200%2520%255Cle%2520e_1%2520%255Cle%2520e_2%2520%255Cle%2520...%2520%255Cle%2520e_m%2520%253D%2520n&dl=0
[第二种表示]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520%2528%2528p_1%252Ce_1%2529%252C%2528p_2%252Ce_2%2529%252C...%252C%2528p_m%252Ce_m%2529%2529&dl=0
[相乘]:https://latex.vimsky.com/test.image.latex.php?fmt=svg&val=%255Cdpi%257B150%257D%2520%255Cfootnotesize%2520M%2528x%2529%2520%253D%2520A%2528x%2529%2520%255Ctimes%2520B%2528x%2529%2520%253D%2520A%2528x%2529%2520%255Ctimes%2520%255Bb_1x%255E%257Be_1%257D%2520%26plus%3B%2520b_2x%255E%257Be_2%257D%2520%26plus%3B%2520...%2520%26plus%3B%2520b_nx%255E%257Be_n%257D%255D%2520%253D%2520%255Csum_%257Bi%2520%253D%25201%257D%255E%257Bn%257D%2520b_iA%2528x%2529x%255E%257Be_i%257D&dl=0
