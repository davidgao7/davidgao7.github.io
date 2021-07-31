---
title: '曾经的神：Support Vector Machine'
date: 2021-07-30
permalink: /posts/2021/07/svmyyds/
tags:
  - Machine Learning
---
# Intro
最近申请工作的时候被问到了，自己这个菜鸡🐔对国内工作不熟悉加上没有充分准备，感觉回答的不是很好😭，
今天，我们就来好好梳理一下什么是SVM，怎么用，原理和trick～

# Support Vector Machine (Classifier)
suggest readings:
- Alpaydin: 10.3, 13.1, 13.2
- Murphy: 14.5.2.2
- Geron: chapter 5, appendix C

## Alpaydin 阅读笔记
### Geometry of the Linear Discriminant （线性可区分的图像）
- 从一个简单的 two classes 情况开始解析，在这种情况下，单个的区分方程已经足够：
- Discriminant between two classes:
$$
\begin{equation}\label{Discriminant_between_two_classes}
\begin{split}
g(\chi) &= g_1(\chi) - g_2(\chi)\\
        &= ((w_1)^T\chi + w_{10}) - ((w_2)^T\chi + w_{20})\\
        &= (w_1 - w_2)^T\chi + (w_{10} - w_{20})\\
        &= w^T\chi + w_0
\end{split}
\end{equation}
$$
- we choose
$$
\left.
        \begin{matrix}
            C_1,\text{ }g(\chi) > 0\\
            C_2,\text{ }otherwise
        \end{matrix}
\right\}
$$

`weight vector threshold`
- defines a hyperplane where $w$ is the weight vector and $w_0$ is the threshold.

### Decision rule
- choose $C_1$ if $w^T\chi > -w_0$, and choose $C_2$ otherwise. The hyperplane divides the input space into two half-spaces: decision region $R_1$ for $C_1$ and $R_2$ for $C_2$. Any $\chi$ in $R_1$ is on the `positive` side of the hyperplane and any $\chi$ in $R_2$ is on the `negative` side.
![IMG_B352B4820514-1.jpeg](attachment:IMG_B352B4820514-1.jpeg)

### Decision bounduary equation
- Let's take 2 points on the decision surface; that is, $g(\chi_1) = g(\chi_2) = 0$, then
$$
\begin{equation}
\begin{split}
    w^T\chi_1 + w_0 &= w^T\chi_2 + w_0\\
    w^T(\chi_1 - \chi_2) &= 0
\end{split}
\end{equation}
$$
and we see that $w$ is *normal* to any vector lying on the hyperplane. Let's rewrite $\chi$ as
$$
\begin{equation}
    \chi = \chi_p + r\frac{w}{|w|}
\end{equation}
$$
- $\chi_p$: normal projection of $\chi$ onto the hyperplane
- $r$: the distance from $\chi$ to the hyperplane
    - $<0$ if $\chi$ is on the negative side
    - $>0$ if $\chi$ is on the positive side

![IMG_686E4B07D60D-1.jpeg](attachment:IMG_686E4B07D60D-1.jpeg)

### Linear Discriminant

- Generative vs. Discriminative
    * Generative model
        - lkj

### Support Vector Machine (SVM)

### Primal & Dual Unconstrained Optimization


```python

```
