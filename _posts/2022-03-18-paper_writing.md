---
layout: post
title: "How to write in English (1)"
description: "found in papers"
categories: [Writing]
tags: [Notes]
redirect_from:
  - /2022/03/18/
---

... `conveys` that ...

As `sketched` in Section 2, ...

We `hereby` provide a quick `sketch`.

We demonstrate that ...

Table 2 `presents` the split for four DML losses.

This link can be `drawn` from two different perspectives, ...

This information theoretic argument `reinforces` our conclusion ...

... `highlight` the fact that ...

the preliminary experiments we provide in the supplementary material indicate that CE and SPCE `exhibit` similar behaviors at training time.

`Throughout` this paper, we `revealed` non-obvious relations between the cross-entropy loss, widely `adopted` in classification tasks, and pairwise losses commonly used in DML.

This connection becomes particularly `apparent` when writing mutual information in both its generative and discriminative views.

We `concede` that ... (尽管不情愿但也得承认)

---

- Datasets are divided into train and evaluation `splits`.
- In-Shop is divided into a query and a gallery `set`.

Recently, `substantial` research efforts ... focused on ...

Specifically, the current `paradigm` is to ...

The recent success of deep neural networks at learning complex, nonlinear mappings of high-dimensional data `aligns with` the problem of learning a suitable embedding.

`While such formulations seem intuitive`, ...

`Admittedly`, the `objective` of doing ...

... `most likely due to its apparent irrelevance` for ...

`To the best of our knowledge`, ...

We show that four of the most `prominent` pairwise metric-learning losses...

... establish tight links between ... and ...

an upper bound on ...

... `represents a proxy` for ...

We consistently obtained `state-of-the-art` results, `outperforming` many recent and complex DML methods.

The tightness part encourages
samples from the same class to be close to each other and form tight clusters. `As for` the contrastive part, it forces samples from different classes to stand `far apart from` one another in the embedded feature space.

This bound is tight when ...

A similar analysis can `be carried out on` other

Lemma 1

> 引理 1

sth. is exhaustively studied in ...

We now completely `change gear to` focus on the widely used unary classification loss: cross-entropy.

On the surface, ...

intractable

auxiliary function

proposition

> 观点，主张，命题

Proposition 1 `casts a new light on` the cross-entropy loss `by` ...

i.e. = id est

In `echo` to Lemma 1, ...

In order to remove the `dependence upon` λ ...

Contrary to ...

This fact `alone` is not enough to explain why the cross-entropy is able to `consistently` achieve better results than DML losses as shown in Section 5.

be substantially easier

it simplifies the implementation, `thus` increasing its potential applicability `in real-world problems`.

---

[1] Boudiaf, M., Rony, J., Ziko, I. M., Granger, E., Pedersoli, M., Piantanida, P., & Ayed, I. B. (2020, August). A unifying mutual information view of metric learning: cross-entropy vs. pairwise losses. In European conference on computer vision (pp. 548-564). Springer, Cham.
