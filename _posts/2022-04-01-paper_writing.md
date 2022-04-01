---
layout: post
title: "How to write in English (2)"
description: "found in papers"
categories: [Writing]
tags: [Notes]
redirect_from:
  - /2022/04/01/
---

`The last decade has witnessed` an experimental revolution in data science and machine learning, `epitomised by` deep learning methods.

`Remarkably`, the `essence` of deep learning is built from two simple algorithmic principles: ...

> Remarkably & obviously

This text is concerned with `exposing` these regularities through unified geometric principles that can `be applied throughout a wide spectrum of applications`.

Deep learning systems are `no exception`, and since the early days researchers have adapted neural networks to exploit the low-dimensional geometry `arising from` physical measurements.

Throughout our `exposition` ...

... provide principled way to build future architectures `yet to be invented`.

`Before proceeding,` `it is worth noting that` our work concerns representation learning architectures and exploiting the symmetries of data `therein`.

`That being said,` we believe
that the principles we will focus on are of significant importance in all of these areas.

`Rather`, we `study` several well-known architectures `in-depth`.

Modern deep learning systems typically operate in the `so-called` interpolating regime.

Inductive Bias `via` Function Regularity.

Modern machine learning `operates` (uses) with large, high-quality datasets ...

Universal Approximation, however, `does not imply an absence of` inductive bias.

we are looking for the most regular functions `within` our hypothesis class.

in many applications with even `modest` dimension d ...

Fully-connected neural networks define function spaces that `enable` more flexible notions of regularity, obtained by considering complexity functions c on their weights.

Whenever possible, we will `omit` the range C `for brevity`.

the domain Ω is usually `endowed` with certain geometric structure and symmetries.

Extending these ideas to other domains such as graphs and manifolds and showing how geometric priors emerge from fundamental principles is the main goal of Geometric Deep Learning and the `leitmotif` of our text.

Symmetries are `ubiquitous` in many machine learning tasks.

The reason is that if both transformations leave the object invariant, then `so does the composition of transformations,` and hence the composition is also a symmetry.

Since these objects will be a `centerpiece` of the mathematical model of Geometric Deep Learning, they deserve a formal definition and detailed discussion

an `equilateral` triangle

`infinitesimal` displacements

For instance, the `aforementioned` group of rotational and reflection symmetries of a triangle is the same as the group of permutations of a sequence of three elements.

We shall see `numerous` instances of group actions in the following sections.

It maps pairs of connected nodes to pairs of connected nodes, and `likewise` for pairs of non-connected nodes.

in computer vision, we might assume that planar translations are exact symmetries. However, the real world is noisy and `this model falls short in two ways`. Firstly, ... Secondly, ...

the setting where the domain $\Omega$ `is fixed`, and signals $x\in\mathcal{X}(\Omega)$ are `undergoing` deformations.

Its `utility` in applications depends on introducing an appropriate deformation cost.

`Canonical` instances of this are applications dealing with graphs and manifolds.

we define ... as the `ensemble` of possible input signals

`As it turns out`, ...

---

[1] sBronstein, M. M., Bruna, J., Cohen, T., & Veličković, P. (2021). Geometric deep learning: Grids, groups, graphs, geodesics, and gauges. arXiv preprint arXiv:2104.13478.
