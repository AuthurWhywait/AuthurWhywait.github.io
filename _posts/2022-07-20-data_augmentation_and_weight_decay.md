---
layout: post
title: "Data Augmentation and Weight Decay"
description: "two ways to make the model generalized well"
categories: [DeepLearning]
tags: [Notes]
redirect_from:
  - /2022/07/20/
---

- Content
{:toc}

## Data Augmentation

Data augmentation refers to randomly applying various kinds of transforms to the images in our dataset. These transforms help introduce more variety in our dataset.

What we do is, instead of feeding the model with the same pictures every time, we do small random transformations (a bit of rotation, zoom, translation, etc…) that doesn’t change what’s inside the image (for the human eye) but changes its pixel values. Models trained with data augmentation will then generalize better. Data augmentation is also useful in situations when you have a relatively small number of training samples.

## Weight Decay

Data augmentation helps deep learning models generalized well, and it's on the data side of the things. Weight Decay is a method **on the model side of things**.

Having fewer parameters is only one way of preventing our model from getting overly complex. But it is actually a very limiting strategy. **More parameters mean more interactions between various parts of our neural network. And more interactions mean more non-linearities. These non-linearities help us solve complex problems.**

One way to penalize complexity, would be to add all our parameters (weights) to our loss function. Well, that won’t quite work because some parameters are positive and some are negative. So what if we add the squares of all the parameters to our loss function. We can do that, however it might result in our loss getting so huge that the best model would be to set all the parameters to 0.

To prevent that from happening, we multiply the sum of squares with another smaller number $wd$.

for loss function:

$$
Loss = MSE(\hat{y}-y) + wd\times sum(w^2)
$$

when updating weights using gradient descent, the derivation of the second term w.r.t. would be: $2\cdot wd\cdot w$. Then from now on, we would not only subtract the learning rate times gradient from the weights but also $2\cdot wd\cdot w$. We are subtracting a constant times the weight from the original weight. This is why it is called weight decay.

Generally a `wd = 0.1` works pretty well.

## Reference

- [Data augmentation using fastai](https://towardsdatascience.com/data-augmentations-in-fastai-84979bbcefaa)
- [This thing called Weight Decay](https://towardsdatascience.com/this-thing-called-weight-decay-a7cd4bcfccab)
