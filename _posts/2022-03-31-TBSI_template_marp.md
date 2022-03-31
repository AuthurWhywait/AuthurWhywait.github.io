---
layout: post
title: "Template for TBSI pre using Marp"
description: "Write up the Assignments and their answers"
categories: [Template]
tags: [Template, Marp]
redirect_from:
  - /2022/03/31/
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

## 写在前面

做演示的方式有很多。本人使用过的相关方式有：

- PowerPoint
- $\LaTeX$
- reveal.js
- impress.js
- Marp

说一下各种方法的优缺点：

- PowerPoint是最普遍的，然而因为本人略有强迫症，总是会执着于页面的布局，导致在使用该软件时，会消耗大量的时间在非内容本身；
- $\LaTeX$为本科毕设导师推荐，推荐一个平台——[Overleaf](https://www.overleaf.com/project)，不管是写论文还是写课程作业都是一把好手，但是对于做演示文稿而言，有些大材小用；
- reveal.js 和 impress.js 是在摸鱼的时候发现的。 reveal.js 完全就是极简主义的代表；而impress.js 是真的 amazing 啊，但是需要强大的三维空间想象能力和脑洞，才能做出美轮美奂的演示。缺点是全程使用html（自动补全是必备）。另外这两个框架都得在包含css的文件夹里面运行，这就导致了一件尴尬的事情，比如说学校要求交演示文稿的ppt，别人都是一个pdf或者ppt，只有你交了一个文件夹。。。另外impress.js还对浏览器有要求。。。
- 而Marp就很舒服了呀，主要使用Markdown（对于博客老手来说简直是超级无敌大福利啊），打个数学公式啥的毫无难度，各种奇怪的字体类似 $\mathfrak{G},\mathbb{G}$ 手到擒来，如果需要复杂一点的渲染，我们可以使用html来补上，但是对于学术演示而言，不需要那么多花里胡哨的红橙黄绿青蓝紫，所以Marp简直是为学术演示而生！

初来TBSI，学院也有自己的ppt模板，但是ppt并不适合我本身，于是用marp写了一个模板，最后效果和学院给的类似。

## 预览

<iframe src="https://authurwhywait.github.io/pdfs/template_TBSI.pdf" style="width:95%; height:1000px;" frameborder="0"></iframe>

## 源码

    ---
    marp: true
    size: 16:9
    ---

    <style>
        footer {
            bottom: 30px;
        }
    </style>

    ![bg](img/TBSI_slides_cover.jpg)

    <!-- _footer: Author: LI Chen, TBSI -->

    <div align=center>

    # <!-- fit --> <font color="#f6e0e0">Template for TBSI pre <br/>using Marp</font>

    <!-- <div align=center><font color="black"><b>Presenter</b>: </font><br/><font color="black"><b>Stu. ID</b>: XXXXXXXXXX</font></div> -->

    **Presenter**: Your Name
    **Date**: xxxx.xx.xx

    </div>

    ---

    # Background - 1

    <!-- ![bg right](img/TBSI_slides_cover.jpg) -->
    ![bg right](img/Gate.png)

        ![bg left]()
        ![bg right]()

    ---

    # Background - 2

    <!-- _footer: Collected from: https://marpit.marp.app/image-syntax -->

    Filters are easily reachable in Marp.

    ![bg left invert:50% drop-shadow:0,5px,10px,rgba(0,0,0,.4) sepia:1.0](img/Gate.png)

        ![blur:10px]()
        ![brightness:1.5]()
        ![contrast:200%]()
        ![drop-shadow:0,5px,10px,rgba(0,0,0,.4)]()
        ![grayscale:1]()
        ![hue-rotate:180deg]()
        ![invert:100%]()
        ![opacity:.5]()
        ![saturate:2.0]()
        ![sepia:1.0]()

    ---

    <!-- 
    paginate: true
    -->

    ![bg](img/TBSI_slides_pattern.png)

    # Font

    - the color of the text can be changed: <font color="purple">texttext</font> <font color=FF00FF>texttext</font> <font color="blue">texttext</font>
    - the size of font can be modified as well: <small>text</small>, text, <big>text</big>, <big><big>text</big></big>, <big><big><big>text</big></big></big>

    ---

    ![bg](img/TBSI_slides_pattern.png)

    # Images - 1

    Single image

    <div align=center><img src="img\curse of dimensionality.png" width="60%"/><br/><small><b>figure 1</b>: the curse of dimensionality</small></div>

    ---

    ![bg](img/TBSI_slides_pattern.png)

    # Image - 2

    Image matrix

    <table align=center border="0">
        <tr align=center>
            <td><img src="img\curse of dimensionality.png" width="90%"/></td>
            <td><img src="img\curse of dimensionality.png" width="60%"/></td>
        </tr>
        <tr align=center>
            <td><img src="img\curse of dimensionality.png" width="50%"/></td>
            <td><img src="img\curse of dimensionality.png" width="80%"/></td>
        </tr>
    </table>

    ---

    ![bg](img/TBSI_slides_pattern.png)

    # Formula

    Inline formula can be realized by `$$`, like $y=x+1$, while letters like these can also be shown in slides: $\mathcal{X}, \mathfrak{G}, \mathit{R}, \mathbb{C}$.

    Formula between lines:

    $$
    y=x+1
    $$

    If we want a formula with process, it's a good idea to align the `=` to make it look nice, like:

    $$
    \begin{aligned}
        y&=x+1\\
        &=3
    \end{aligned}
    $$

    ---

    ![bg](img/TBSI_slides_pattern.png)

    # Footer

    footer only works on this slide: `<!-- _footer: Citation &nbsp;|&nbsp; Name &nbsp; | &nbsp;institution &nbsp;|&nbsp; Date-->`

    footer works from this slide: `<!-- footer: Citation &nbsp;|&nbsp; Name &nbsp; | &nbsp;institution &nbsp;|&nbsp; Date-->`

    <!-- _footer: Citation &nbsp;|&nbsp; Name &nbsp; | &nbsp;institution &nbsp;|&nbsp; Date-->

    ---

    ![bg](img/TBSI_slides_pattern.png)

    # Code

    ```python
    year = int(raw_input('year:\n'))
    month = int(raw_input('month:\n'))
    day = int(raw_input('day:\n'))

    months = (0,31,59,90,120,151,181,212,243,273,304,334)
    if 0 <= month <= 12:
        sum = months[month - 1]
    else:
        print 'data error'
    sum += day
    leap = 0
    if (year % 400 == 0) or ((year % 4 == 0) and (year % 100 != 0)):
        leap = 1
    if (leap == 1) and (month > 2):
        sum += 1
    print 'it is the %dth day.' % sum
    ```

    ---

    ![bg](img/TBSI_slides_pattern.png)

    # List

    bullet list

    ```markdown
    - One
    - Two
    - Three
    ```

    ordered list

    ```markdown
    1. One
    2. Two
    3. Three
    ```

    ---

    ![bg](img/TBSI_slides_pattern.png)

    # Table

    A common table:

    <div align=center>

    | |1|2|4|5|6|7|8|
    |-|-|:-|-|:-:|-|-:|-|
    |1|2|7|sdfe|123|2|7|3|
    |2|4|5daf|9|2|4|5dfs|6|

    <small>Table 1: example</small>

    </div>

    If we want to set the format of the table with more complexity, we should use `html` as tools.
