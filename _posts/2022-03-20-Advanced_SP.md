---
layout: post
title: "Signal Processing Assignments 01"
description: "Write up the Assignments and their answers"
categories: [SignalProcessing]
tags: [Notes, Signal Processing]
redirect_from:
  - /2022/03/20/
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

## LTI systems?

$$
ae_1(t)+be_2(t)\rightarrow ai_1(t)+bi_2(t)\tag{step 1: Linearity}
$$

$$
e(t-t_0)\rightarrow i(t-t_0)\tag{step 2: Time Invariant}
$$

i.e. If $y[n]=\frac{1}{2n_0+1}\sum_{k=n-n_0}^{n+n_0}x[k]$ is a LTI system?

<div align=center><img src="https://cdn.jsdelivr.net/gh/AuthurWhywait/images/20220318231717.png" width="500"/></div>

## properties of Convolution

$$f(t)\ast g(t)=\int_{-\infty}^{+\infty}f(\tau)g(t-\tau)d\tau\tag{Def.}$$

$$f(t)\ast g(t)=g(t)\ast f(t)\tag{Commutative law}$$

$$f(t)\ast (g(t)+h(t))=f(t)\ast g(t)+f(t)\ast h(t)\tag{Distributive law}$$

$$(f(t)\ast g(t))\ast h(t)=f(t)\ast (g(t)\ast h(t))\tag{Associative law}$$

$$f(t)\ast\delta(t-t_0)=f(t-t_0)\tag{with Dirac Function}$$

$$
\begin{cases}
    f(t)\ast g(t-t_0)=f(t-t_0)\ast g(t-t_0)\\
    f(t-t_0)\ast g(t)=f(t-t_0)\ast g(t-t_0)
\end{cases}
\tag{Displacement characteristics}
$$

$$
\begin{cases}
    a\cdot(f(t)\ast g(t))=(a\cdot f(t))\ast g(t)\\
    a\cdot(f(t)\ast g(t))=f(t)\ast (a\cdot g(t))\\
\end{cases},~a\in\mathcal{R}-\{0\}\tag{scaling 1}
$$

$$
(f(a\cdot\tau)\ast g(a\cdot\tau))(t)=\frac{1}{\vert a\vert}\cdot (f(\tau)\ast g(\tau))(a\ast t)\tag{scaling 2}
% f(a\cdot t)\ast g(a\cdot t)=\frac{1}{\vert a\vert}\cdot f(t)\ast g(t), ~a\in\mathcal{R}-\{0\}\tag{scaling 2}
$$

$$
\begin{cases}
    (f(t)\ast g(t))'=f(t)\ast g'(t)\\
    (f(t)\ast g(t))'=f'(t)\ast g(t)
\end{cases}\tag{Differential properties}
$$

$$f(t)\ast u(t)=\int_{-\infty}^tf(\tau)d\tau\tag{with unit step function}$$

$$
\int_{-\infty}^tf(\tau)\ast g(\tau)d\tau=[\int_{-\infty}^tf(\tau)d\tau]\ast g(t)\tag{integral property}
$$

### some proofs

<table><tr><td bgcolor="gray">The Main idea of the proofs for the former properties is using both the definition and the method of substitution.</td></tr></table>

i.e. Displacement characteristics:

$$
\begin{aligned}
    LHS&=[f(\tau)\ast g(\tau-t_0)](t)\\
    &=[g(\tau-t_0)\ast f(\tau)](t)\\
    &=\int g(\tau-t_0)f(t-\tau)d\tau\\
    &=\int g(\epsilon)f(t-t_0-\epsilon)d\tau\\
    &=[g(\epsilon)\ast f(\epsilon)](t-t_0)\\
    &=f(t-t_0)\ast g(t-t_0)
\end{aligned}
$$

## Fourier Series

$$
\begin{aligned}
    x_0(t)=&\frac{a_0}{2}+\sum_{n=1}^\infty[a_n\cos(nt)+b_n\sin(nt)]\\
    &\begin{cases}
        a_0=\frac{2}{T}\int_{-\frac{T}{2}}^{\frac{T}{2}} x(t)dt\\
        a_n=\frac{2}{T}\int_{-\frac{T}{2}}^{\frac{T}{2}} x(t)\cos(nt)dt\\
        b_n=\frac{2}{T}\int_{-\frac{T}{2}}^{\frac{T}{2}} x(t)\sin(nt)dt
    \end{cases}
\end{aligned}
$$

## Useful table

<!-- <center><embed src="/pdf/fourier.pdf" width="850" height="600"></center> -->

<!-- <object :src="/pdf/fourier.pdf" width="100%" height="100%">
    This browser does not support PDFs. Please download the PDF to view it: <a :href="/pdf/fourier.pdf">Download PDF</a>
</object> -->

<!-- <iframe src="https://ethz.ch/content/dam/ethz/special-interest/baug/ibk/structural-mechanics-dam/education/identmeth/fourier.pdf" style="width:95%; height:55%;" frameborder="0"></iframe> -->

<iframe src="_posts\pdf\fourier.pdf" style="width:95%; height:55%;" frameborder="0"></iframe>
