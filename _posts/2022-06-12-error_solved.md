---
layout: post
title: "【Error】RuntimeError: CUDA error: no kernel image is available for execution on the device"
description: "error solving"
categories: [Debug]
tags: [Ubuntu, Mac]
redirect_from:
  - /2022/06/12/
---

## 场景

> GeForce RTX 3090, Ubuntu 20.

欲跑通YOLOv5的官方代码，[colab notebook 链接在此](https://colab.research.google.com/github/ultralytics/yolov5/blob/master/tutorial.ipynb)，在运行以下命令行时，

```command
python detect.py --weights yolov5s.pt --img 640 --conf 0.25 --source data/images
```

出现如下报错

<font color='red'>RuntimeError: CUDA error: no kernel image is available for execution on the device</font>

## 主要的解决方法

网上的主流方法是解决Pytorch中注意CUDA版本和GPU算力匹配的问题。我们只要让版本匹配就ok，下面随便给一个[相关连接](https://blog.csdn.net/m0_46483236/article/details/124112298)。

## 另外的解决方法

问题出在函数`select_device()`函数上，打开此函数的定义，我们可以看到如下代码：

```python
cpu = device == 'cpu'
mps = device == 'mps'  # Apple Metal Performance Shaders (MPS)
```

而实验室的服务器为Ubuntu20系统，并非苹果系统，只有cpu和gpu。所以最简单的方法就是将``函数中的所有'mps'或者'MPS'分别换成'gpu'和'GPU'即可。

> 关于 [Apple Metal Performance Shaders (MPS)](https://developer.apple.com/documentation/metalperformanceshaders)

<font color=red>问题解决！</font>
