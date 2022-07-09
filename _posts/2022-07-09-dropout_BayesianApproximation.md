---
layout: post
title: "Tricks in Cost Function, Error Measurements, ELBO,  Gaussian Process, Monte Carlo Integration"
description: ""
categories: [DeepLearning]
tags: [Notes]
redirect_from:
  - /2022/07/09/
---

- Content
{:toc}

## Tricks in Squared Error Cost Function

**Why do we have to divide by 2 in the ML squared error cost function?**

Cost Function:

$$
E = \frac{1}{2N}\sum_{i=1}^m\Vert \bf{y}_n -\hat{\mathbf{y}}_n\Vert^2_2
$$

It is simple. It is because when you take the derivative of the cost function, that is used in updating the parameters during gradient descent, that 2 in the power get cancelled with the 12 multiplier, thus the derivation is cleaner. These techniques are or somewhat similar are widely used in math in order "To make the derivations mathematically more convenient". You can simply remove the multiplier, see here for example, and expect the same result.

## Different error measurements

To use the NN model for regression, we might use the Euclidean loss (also known as "squared loss"),

$$
E = \frac{1}{2N}\sum_{i=1}^m\Vert \mathbf{y}_n -\hat{\bf{y}}_n\Vert^2_2
$$

where $\{\mathbf{y}_1,...,\mathbf{y}_n\}$ are $N$ outputs, and $\{\hat{\bf{y}}_1,...,\hat{\mathbf{y}}_n\}$ being the outputs of hte model with corresponding observed inputs $\{\mathbf{x}_1,...,\mathbf{x}_n\}$.

To use the model for classification, predicting the probability of $\bf{x}$ being classified with label $1, ..., D$, we pass the output of the model $\hat{y}$ through an element-wise softmax function to obtain normalized scores:

$$
\hat{p}_{nd}=\frac{\exp(\hat{y}_{nd})}{\sum_{d'}\exp(\hat{y}_{nd'})}.
$$

Taking the log of this function results in a softmax loss,

$$
E=-\frac{1}{N}\sum_{n=1}^N\log (\hat{p}_n, c_n)
$$

where $c_n\in[1,2,...,D]$ is the observed class for input $n$.

## Evidence Lower Bound (ELBO)

$$
\log P(X) \ge E_{Z\sim Q}[\log\frac{P(X,Z)}{Q(Z)}]
$$

## Gaussian Process

The Gaussian Process offers desirable properties:

- uncertainty estimates over the function values,
- robustness to over-fitting,
- and principled ways for hyper-parameter tuning.

## Marginal and Conditional Gaussians

Given a marginal Gaussian distribution for $x$ and a conditional Gaussian distribution for $y$ given $x$ in the form

$$
\begin{aligned}
    p(\mathbf{x}) &= \mathcal{N}(\mathbf{x}\vert\mu,\Lambda^{-1})\\
    p(\mathbf{y}\vert\mathbf{x}) &= \mathcal{N}(\mathbf{y}\vert\mathbf{Ax+b},\mathbf{L}^{-1})
\end{aligned}
$$

the marginal distribution of $\mathbf{y}$ and the conditional distribution of $\mathbf{x}$ given $\mathbf{y}$ are given by

$$
\begin{aligned}
    p(\mathbf{y})=\mathcal{N}(y\vert\mathbf{A\mu+b, L^{-1}+A\Lambda^{-1}A^T})\\
    p(\mathbf{x}\vert\mathbf{y}) = \mathcal{N}(\mathbf{x}\vert\mathbf{\Sigma\{A^TL(y-b)+\Lambda\mu\},\Sigma})
\end{aligned}
$$

where

$$
\mathbf{\Sigma} = (\mathbf{\Lambda + A^TLA})^{-1}.
$$

## Product of Gaussian Densities

Let $\mathcal{N}(\mathbf{m,\Sigma})$ denote a density of $\mathbf{x}$, then

$$
\mathcal{N}_\mathbf{x}(\mathbf{m_1,\Sigma_1})\cdot\mathcal{N}_\mathbf{x}(\mathbf{m_2,\Sigma_2})=c_c\mathcal{N}_\mathbf{x}(\mathbf{m_c, \Sigma_c})
$$

while

$$
\begin{cases}
    c_c &= \mathcal{N}_{m_1}(m_2, (\Sigma_1+\Sigma_2))\\
    &= \frac{1}{\sqrt{\det(2\pi(\Sigma_1+\Sigma_2))}}\exp[-\frac{1}{2}(\mathbf{m_1-m_2})^T(\Sigma_1+\Sigma_2)^{-1}(\mathbf{m_1-m_2})]\\
    \mathbf{m}_c &= (\Sigma_1^{-1}+\Sigma_2^{-1})^{-1}(\Sigma_1^{-1}\mathbf{m}_1+\Sigma_2^{-1}\mathbf{m}_2)\\
    \Sigma_c &= (\Sigma_1^{-1}+\Sigma_2^{-1})^{-1}
\end{cases}
$$

<font color=red>

but note that the product is not normalized as a density of $\mathbf{x}$.

</font>

## Monte Carlo integration

In mathematics, Monte Carlo integration is a technique for numerical integration using random numbers. It is a particular Monte Carlo method that numerically computes a definite integral. While other algorithms usually evaluate the integrand at a regular grid, Monte Carlo randomly chooses points at which the integrand is evaluated. This method is particularly useful for higher-dimensional integrals.

## References

- [Dropout as a Bayesian Approximation: Appendix](https://arxiv.org/abs/1506.02157)
- [Bishop - Pattern Recognition and Machine Learning](https://docs.google.com/viewer?a=v&pid=sites&srcid=aWFtYW5kaS5ldXxpc2N8Z3g6MjViZDk1NGI1NjQzOWZiYQ)
- [Matrix-cookbook](http://compbio.fmph.uniba.sk/vyuka/ml/old/2008/handouts/matrix-cookbook.pdf)
- [Monte Carlo integration](https://en.wikipedia.org/wiki/Monte_Carlo_integration)
