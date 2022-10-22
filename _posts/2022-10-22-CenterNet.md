---
layout: post
title: "CenterNet. Objects as Points"
description: "CenterNet"
categories: [PaperReading]
tags: [Object Detection, CenterNet]
redirect_from:
  - /2022/10/22/
---

This paper represents objects by a single point at their bounding box center. Object detection is then a standard keypoint estimation problem.

> Other properties, such as object size, dimension, 3D extent, orientation, and pose are then regressed directly from image features at the center location.

The input image are fed to a fully convolutional network that generates a heatmap. Peaks in this heatmap correspond to object centers. Image features at each peak predict the object bounding box height and weight. The model trains using standard dense supervised learning. Inference is a single network forward-pass, without non-maximal suppression for post-processing.

Other used techniques:

- simple Resnet-18
- up-convolutional layers
- DLA-34 (deep layer aggregation, a key keypoint detection network)
- Hourglass-104 (keypoint estimation network)
- multi-scale testing

---

- Content
{:toc}

## Loss function

<!-- ## Preliminary -->

> $p\in\mathcal{R}^2$ of class $c$;
> low-resolution equivalent $\tilde{p}=\left\lfloor\frac{p}{R}\right\rfloor$;
> heatmap $Y \in[0,1]^{\frac{W}{R} \times \frac{H}{R} \times C}$
> Gaussian kernel $Y_{x y c}=\exp \left(-\frac{\left(x-\tilde{p}_{x}\right)^{2}+\left(y-\tilde{p}_{y}\right)^{2}}{2 \sigma_{p}^{2}}\right)$

The training objective is a penalty-reduced pixel-wise logistic regression with focal loss:

$$
L_{k}=\frac{-1}{N} \sum_{x y c}\left\{\begin{array}{cl}
\left(1-\hat{Y}_{x y c}\right)^{\alpha} \log \left(\hat{Y}_{x y c}\right) & \text { if } Y_{x y c}=1 \\
\left(1-Y_{x y c}\right)^{\beta}\left(\hat{Y}_{x y c}\right)^{\alpha}
\log \left(1-\hat{Y}_{x y c}\right) & \text { otherwise }
\end{array}\right.
$$

> additionally predict a local offset $\hat{O}\in\mathcal{R}^{\frac{W}{R}\times\frac{H}{R}\times 2}$

All classes $c$ share the same offset prediction. The offset is trained with an L1 loss

$$
L_{off}=\frac{1}{N}\sum_p\vert\hat{O}_{\tilde{p}}-(\frac{p}{R}-\tilde{p})\vert
$$

<!-- ## Object as Points -->

> bounding box: $\left(x_{1}^{(k)}, y_{1}^{(k)}, x_{2}^{(k)}, y_{2}^{(k)}\right)$
> center point: $p_k = \left(\frac{x_{1}^{(k)}+x_{2}^{(k)}}{2}, \frac{y_{1}^{(k)}+y_{2}^{(k)}}{2}\right)$
> regress to the object size $s_{k}=\left(x_{2}^{(k)}-x_{1}^{(k)}, y_{2}^{(k)}-y_{1}^{(k)}\right)$ for each object $k$
> single prediction $\hat{S} \in \mathcal{R}^{\frac{W}{R} \times \frac{H}{R} \times 2}$ for all object categories.

Use an L1 loss at the center point similar to Object:

$$
L_{size}=\frac{1}{N} \sum_{k=1}^{N}\left|\hat{S}_{p_{k}}-s_{k}\right|
$$

The overall training objective (instead of normalizing the scale and directly use the raw pixel coordinates,  the paper scales the loss by a constant $\lambda_{size}$.):

$$
L_{\text {det}}=L_{k}+\lambda_{size} L_{size}+\lambda_{off} L_{off}
$$

<font color=red>Pay more attention to the diagram in this paper!</font>

## Reference

- Zhou, X., Wang, D., & Krähenbühl, P. (2019). Objects as points. arXiv preprint arXiv:1904.07850.
