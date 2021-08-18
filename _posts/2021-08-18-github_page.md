---
layout: post
title: "GithubPage Skills and Tools"
description: "GithubPage Skills and Tools"
categories: [Collection]
tags: [HTML, Markdown, Latex, Tools, Website]
redirect_from:
  - /2021/08/18/
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

### 关于Latex

【问题一】如何让 github page 支持 markdown 中使用 latex 数学公式插入?

正文开头加上下面代码块：

```html
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
```

【问题二】对于绝对值符号 “$\left |\right |$” 被识别为表格分隔符。例子：$\left |a\right |$

> 行内 latex 公式会出现此问题，行间 latex 并不会出现此问题。

```latex
$\left| a\right|$”
```

【问题三】几个形似符号的区分

- $\Sigma~and~\sum$
- $\to~and~\rightarrow$

```latex
\Sigma~and~\sum
\to~and~\rightarrow
```

【问题四】显示**同括号内公式等高**的括号

```latex
\left(\right)
\left[\right]
\left\{\right\}
```

## 关于图片插入

图片插入方法颇多，但是个人最喜欢的方法是将图片转换为 base64 的格式，然后以如下 html 代码块插入文内（可以调节对齐方式、宽度之类）

```html
<div align=center>
    <img src="source" width="300"/>
</div>
```

- 优点：不用图床；
- 缺点：转出的base64码超级无敌长，会打乱格式（虽然我们可以用markdown语法中的超链接将所有图片的base64码放在文末但是此方法无法调节对齐方式及图片大小）

> 一切都为了颜值！

另外如果使用vscode编辑，文本一长就卡出天际，不知道是不是电脑的配置问题。如果大量插入图片的base64码，建议使用SublimeText进行编辑操作。（总还是要比记事本好一些的）另外关于SublimeText写markdown，点击《[SublimeText3的插件安装方式以及插件MarkdownEditing的安装](https://authurwhywait.github.io/blog/2021/02/23/sublime_text3/)》查看教程。

---

markdown语法和html语法不能水乳交融！！！

---

## 网站推荐

- [图片转base64](https://oktools.net/image2base64)
- [在线latex公式编辑](https://www.latexlive.com/)
