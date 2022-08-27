---
layout: post
title: "Cross Entropy Loss and its Derivations"
description: "An introduction of Cross Entropy and some tricks"
categories: [DeepLearning]
tags: [Trick]
redirect_from:
  - /2022/08/27/
---

- Content
{:toc}

## Cross Entropy Loss

The cross entropy loss of a sample:

$$
L = -[y\log\hat{y}+(1-y)\log(1-\hat{y})]
$$

Here, Logarithm is utilized for the reasons below:

- The logarithmic function preserves the original monotonicity.
- With the increasing difference between prediction and label y, the punishment of the model (loss function) will grow exponentially.

## BCELoss and BCEWithLogitsLoss

BCEWithLogitsLoss = Sigmoid + BCELoss

## Trick

### Trick 1: Label Smoothing

Label smoothing is a trick designed to prevent overfitting in machine learning classification or detection problems.

In common case, the probability of correct prediction will always be $1$, while the incorrect ones will be $0$, which allows the model to maximize the reward for the correct classification and the penalties for incorrect ones. This strategy is definitely ideal if the training data covers all situations perfectly. In practice, however, the perfectness of training data is out of reach, which means that the methodology mentioned above may lead to overfitting.

Therefore, label smoothing is proposed to punish the correct classification slightly, which is actually a regularization strategy to decrease the weights of positive samples when calculating the loss function, and finally prevent overfitting.

**Label Smoothing regularizes a model based on a softmax with $k$ output values by replacing the hard $0$ and $1$ classification targets with targets of $\frac{\epsilon}{k-1}$ and $1-\epsilon$ respectively.**

Binary classification case:

$$
[0, 1] \times (1-\epsilon) + \frac{\epsilon}{2} = [\epsilon, 1-\epsilon]
$$

```python
def smooth_BCE(eps=0.1):   # eps 平滑系数  [0, 1]  =>  [0.95, 0.05]
    # return positive, negative label smoothing BCE targets
    # positive label= y_true * (1.0 - label_smoothing) + 0.5 * label_smoothing
    # y_true=1  label_smoothing=eps=0.1
    return 1.0 - 0.5 * eps, 0.5 * eps
```

### Trick 2: Focal Loss

The strategy of focal loss is to focus more on hard examples, avoiding the loss function dominated by those easy examples.

$$
\text{FL}(p_t) = -\alpha_t(1-p_t)^\gamma\log(p_t)
$$

while
$$
p_t=\begin{cases}
    p&,y=1\\
    1-p&,o.w.
\end{cases} \\
\alpha_t = \begin{cases}
    \alpha & y=1\\
    1-\alpha &o.w.
\end{cases}, \alpha\in[0,1]
$$

$\alpha_t, \gamma$ are all hyperparameters: $\alpha_t$ is a vector of weights that balances the quantities of samples with different labels, and $\gamma$ reduces the loss weight of easy examples and makes the model focus more on hard examples.

Limitations:

- Sensitive to noise: trend to take noise as a hard example.
- Training may be unstable at the early stage of training: larger classes may dominate the loss function.
- Hyperparameters $\alpha_t$ and $\gamma$ are hard to choose: a bad tuning may result in worse effect.

## Reference

- [【trick 1】Label Smoothing（标签平滑）—— 分类问题中错误标注的一种解决方法](https://blog.csdn.net/qq_38253797/article/details/116228065)
- [Label Smoothing](https://paperswithcode.com/method/label-smoothing)
- [Focal Loss for Dense Object Detection](https://arxiv.org/abs/1708.02002)