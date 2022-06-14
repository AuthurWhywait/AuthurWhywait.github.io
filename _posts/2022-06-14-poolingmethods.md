---
layout: post
title: "Popular Pooling methods (1)"
description: "brief review of pooling methods"
categories: [NeuralNetwork]
tags: [Pooling]
redirect_from:
  - /2022/06/14/
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

- Content
{:toc}

## Average Pooling

## Max-Pooling

## Mixed-Pooling

$$
s_j = \lambda\max_{i\in R_j}a_i + (1-\lambda)\frac{1}{\vert R_j\vert}\sum_{i\in R_j}a_i
$$

where $\lambda$ decides the choice of either using max pooling or average pooling. The value of $\lambda$ is selected randomly either 0 or 1.

The value of $\lambda$ is recorded for forward-propagation order it is used during the backpropagation process. It is superiority over max and average pooling by performing image classification on three different datasets.

## $L_p$ Pooling

$$
s_j = (\frac{1}{\vert R_j \vert}\sum_{i\in R_j}a_i^p)^{\frac{1}{p}}
$$

Its generalization ability is better than max pooling.

- $p=1$, $L_p$ operator behaves as average pooling;
- $p=\infty$, it leads to max pooling.

When $p>1$, $L_p$ pooling is examined as a trade-off between average and max pooling.

## Stochastic Pooling

It applies multinomial distribution to pick the value randomly. It can be divided into two steps:

1）Compute the probabilities $p_i$:

$$
p_i=\frac{a_i}{\sum_{k\in R_j}a_k}
$$

2）These probabilities create a multinomial distribution that is used to select location $l$ and corresponding pooled activation $a_l$ based on $p$. Multinomial distribution selects a location $l$ with the region:

$$
s_j = a_l\text{ where }l\sim P(p_1, p_2, p_{\vert R_j\vert})
$$

## Spatial Pyramid Pooling

- popularly known as spatial pyramid matching or SPM.
- one of the most successful methods in computer vision.

It partitions the images into divisions from finer to coarser levels and aggregates local features in them.

The spatial pyramid pooling (SPP) layer can remove the fixed-size constraints of the networks, and it can be added on top of the last convolutional layer. It pools the features and generates fixed-length outputs, which are then fed into the fully-connected layers (or other classifiers).

In other words, we perform some information aggregation at a deeper stage of the network hierarchy (between convolutional layers and fully connected layers) to avoid the need for cropping or warping at the beginning.

## Region of Interest Pooling (RoI)

- The Region of Interest (RoI) Pooling layer is an important component of convolutional neural networks which is mostly used for object detection and segmentation.

RoI Pooling is just a type of max-pooling, where the pool size is dependent on the input size. Doing this ensures that the output is always of the same size.

This layer is used because the fully-connected layer always expects the same input size, but input regions to the FC layer may have different sizes.

> For example, to detect multiple cars and pedestrians in a single image. Its purpose is to perform max pooling on inputs of nonuniform sizes to obtain fixed-size feature maps.
