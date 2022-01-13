---
layout: post
title: "Github: Failed to connect to 127.0.0.1 port 10809: Connection refused"
description: "github desktop 上传及下载问题"
categories: [Github]
tags: [Problem Solving]
redirect_from:
  - /2022/01/14/
---

## 问题

`Failed to connect to 127.0.0.1 port 10809: Connection refused`

## 解决方案

网上解决方案有很多，但大多都指出问题出现在代理 proxy 上。具体解决步骤大同小异，详情点击链接跳转：

- [解决出现Failed to connect to 127.0.0.1 port XXXX: Connection refused](https://blog.51cto.com/u_15326986/3328702)

但是，多次尝试之后，此通常的解决方案对我的情况并不起作用。即使多次重启软件 `github desktop` 甚至重启电脑，都于我的情况无用。

最终我将本地仓库删了之后，重新从 github 上把整个代码库 clone 下来，此问题就消失了。

---

> 属于是菜鸡的玄学操作了。
