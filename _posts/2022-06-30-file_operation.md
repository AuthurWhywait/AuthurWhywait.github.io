---
layout: post
title: "Python 随机选取指定数量的文件并寻找他处的同名文件"
description: "Python 随机选取指定数量的文件并寻找他处的同名文件"
categories: [Python]
tags: [File, Code]
redirect_from:
  - /2022/06/30/
---

> 使用场景: 分离数据集

## 目标

1. 从文件夹 dir0/images 随取抽取指定数量的图片, 将其复制到文件夹 target_dir/images 后, 删除被复制过的文件.
2. 在文件夹 dir0/labels 中, 寻找已经复制到文件夹 target_dir/images 的同名文件 (只是后缀名不同), 将其复制到 target_dir/labels 中, 然后在 dir0/labels 中将其删除.

## 文件夹结构

    + dir0
      + images
        + 0.jpg
        + 1.jpg
        + ...
      + labels
        + 0.txt
        + 1.txt
        + ...
    + target_dir
      + images
      + labels

## 源码

```python
import os, random, shutil

# sampling 100 images from dir0 to target_dir
# sampling 300 images from dir0 to be the validation set

dir0 = './all_data'
target_dir = './val'

# create the folder if not exits
# os.makedirs(target_dir)

# sampling process
sampling_number = 500
imgs = os.listdir(dir0 + '/images')
sample = random.sample(imgs, sampling_number)

for img in sample:
    # get the path of the image and label
    img_path = dir0 + '/images/' + img
    img_name, img_extension = os.path.splitext(img)
    label_path = dir0 + '/labels/' + img_name + '.txt'
    # copy and delete
    shutil.copy(img_path, target_dir + '/images/')
    os.remove(img_path)
    shutil.copy(label_path, target_dir + '/labels/')
    os.remove(label_path)
```
