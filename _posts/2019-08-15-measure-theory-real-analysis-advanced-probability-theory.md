---
layout: post
title:  "测度论、实分析和高等概率论"
date:   2019-08-15 10:25:00 +0800
author: 西伯利亚虎
categories: math
---

本文简要介绍测度论、实分析和高等概率论的基本概念。

## 测度论

$(\Omega, \mathcal{F}, \mu)$表示一个**测度空间**，其中$\Omega$是某个给定的空间或集合，$\mathcal{F}$是$\sigma$-代数，$\mu$是测度。

### $\sigma$-代数

$\sigma$-代数也称为$\sigma$-域，是由$\Omega$的子集构成的集合，满足：

1.  取补封闭，即$A \in \mathcal{F} \Rightarrow A^c \in \mathcal{F}$；
2.  可列并封闭，即$A_i \in \mathcal{F} \Rightarrow \cup_i A_i \in \mathcal{F}$，可列指有限或无限可列。

由$\cap_i A_i = (\cup_i A_i^c)^c$，可知$\sigma$-代数对可列交也是封闭的。

设$\mathcal{A}$是$\Omega$子集构成的集合，则$\sigma(\mathcal{A})$表示包含$\mathcal{A}$的最小$\sigma$-代数，称为由$\mathcal{A}$生成的$\sigma$-代数。最小$\sigma$-代数是指所有包含$\mathcal{A}$的$\sigma$代数的交集，这里用到了两个$\sigma$-代数的交也是$\sigma$-代数的性质。

### 测度

测度是将$\sigma$-代数映射到实数的函数$\mu: \mathcal{F} \rightarrow \mathbb{R}$，满足

1.  非负且空集映射到0，即对于一切$A\in \mathcal{F}$，有$\mu(A) \ge \mu(\emptyset) = 0$；
2.  可列可加，即对可列且不想交的集合序列$A_i \in \mathcal{F}$，有$\mu(\cup_i A_i) = \sum_i \mu(A_i)$。

### 乘积测度

两个测度可以通过相乘得到一个新的测度，称为**乘积测度**。设测度1的测度空间为$(\Omega_1, \mathcal{F}_1, \mu_1)$，测度2的测度空间为$(\Omega_2, \mathcal{F}_2, \mu_2)$，它们的乘积测度为$(\Omega, \mathcal{F}, \mu)$，则
1.  $\Omega = \Omega_1 \times \Omega_2$是Cartesian积，即
    $$\Omega = \left\{(A_1, A_2): A_1 \in \Omega_1, A_2 \in \Omega_2\right\}$$
    ；
2.  $\mathcal{F} = \sigma(\mathcal{F}_1 \times \mathcal{F}_2)$是由$\mathcal{F}_1$和$\mathcal{F}_2$的Cartesian积生成的$\sigma$-代数；
3.  对于$A_1 \in \Omega_1, A_2 \in \Omega_2$，有$\mu((A_1, A_2)) = \mu_1(A_1) \cdot \mu_2(A_2)$。

## 实分析

实分析传统上也称为实变函数论，研究的测度空间是$(\mathbb{R}^d, \mathcal{L}^d, m)$，其中$\mathcal{R}$是实数域，$\mathcal{L}$是Lebesgue可测集的集合，$m$是Lebesgue测度。为突出概念，我们以下只考虑维数$d = 1$的情况。

### 测度完备化

Borel域是$\mathbb{R}$上所有开集生成的$\sigma$-域，Borel域中的元素称为Borel集。
Lebesgue测度$m(E)$从概念上讲是$E$的长度，例如$m([a, b]) = m((a, b)) = b - a$。
有些Borel集Lebesgue测度为0，但这些零测集的子集有些却不属于Borel域。为了让测度完备化，将Borel域在Lebesgue测度下的零测集的所有子集记作$\mathcal{N}$，令$\mathcal{L} = \sigma(\mathcal{B}\cup \mathcal{N})$，即由$\mathcal{B}$和$\mathcal{N}$并集生成的$\sigma$-代数，则$\mathcal{L}$是所有Lebesgue可测集构成的集合。

### Lebesgue积分

函数$f$ Lebesgue可测是指$f$将$(\mathbb{R}, \mathcal{L})$映射到$(\mathbb{R}, \mathcal{B})$，即Borel集的原象是Lebesgue可测集。

我们研究Lebesgue可测的函数的Lebesgue积分。Lebesgue积分的定义基于简单函数，即形如$f = \sum_{i=1}^n a_i I_{A_i}$的函数，其中$I_{A_i}$是$A_i$的示性函数。简单函数的Lebesgue积分定义为

$$
\int_{\mathbb{R}} f \text{d}m = \sum_{i=1}^n a_i m(A_i).
$$

对于非负Lebesgue可测函数，Lebesgue积分定义为

$$
\int_{\mathbb{R}} f \text{d}m = \sup \left\{ \int_{\mathbb{R}} g \text{d}m: g\text{非负简单且} g \le f \right\}.
$$

这可以看作是对$f$作横线切割，投影到$x$轴上找到找到原象的测度再加和，切割越密，越逼近$f$与$x$轴围成的面积，这一极限就是Lebesgue积分。Riemann积分是竖着积，Lebesgue积分是横着积，说的就是这个意思。

对于有正有负的Lebesgue可测函数，我们将函数分为正负两个部分，将负的部分翻到$x$轴以上作Lebesgue积分后，再用正的部分的积分减去负的部分翻转后的积分。

Lebesgue积分扩大了可积函数的范围，例如在有理数上取1、无理数上取0的Dirichlet函数因为Darboux上和与Darboux下和不等而Riemann不可积，但却Lebesgue可积，显然其Lebesgue积分为有理数集$\mathbb{Q}$的Lebesgue测度。有理数集是可列集，而一切可列集的Lebesgue测度都为0，因为设可列集为$\{a_i\}_{i=1}^{\infty}$，则考虑集合

$$
A_k = \cup_{i=1}^{\infty} (a_i - \frac{1}{2^k}, a_i + \frac{1}{2^k}), \quad k = 1, 2, \cdots
$$

我们知道，$m(A_k) = \frac{1}{2^{k-1}}$，因而可列集的Lebesgue测度$=\lim_{k\rightarrow \infty} m(A_k) = 0$。

需要指出，也不是所有Riemann可积的函数都Lebesgue可积。正部和负部的反常Riemann积分都是无穷的函数Lebesgue不可积。当Riemann积分和Lebesgue积分都存在时，二者相等。

## 高等概率论

概率论的测度空间是$(\Omega, \mathcal{F}, P)$，其中$P$是概率测度，相比一般测度的特别之处是$P(\Omega) = 1$。

随机变量$X: (\Omega, \mathcal{F}) \rightarrow (\mathbb{R}, \mathcal{B})$是从$\Omega$到$\mathbb{R}$的可测函数，这里的可测是指Borel集的原象$\in \mathcal{F}$。

### $L_p$空间

一般定义在$(\Omega, \mathcal{F}, \mu)$上的可测函数的$L_p$范数定义为

$$
\|f\|_p = \sqrt[p]{\int_{\Omega} f \text{d}\mu}.
$$

据此，随机变量$X$的$L_p$范数是$(\mathbb{E}[X^p])^{\frac{1}{p}}$。这一定义对连续与离散的随机变量均适用。顺便指出，$\mathbb{R}^d$中向量范数的定义是可测函数$L_p$范数的定义的特例，即把$d$维向量看作是$([d], [d]的\text{所有子集}) \rightarrow (\mathbb{R}, \mathcal{B})$的可测函数，且在原象空间的测度是$\mu_{\text{card}}$。$[d]$是指$\{n\in \mathbb{N}^+: n \le d\}$。

$(\Omega, \mathbb{F}, P)$上所有$L_p$范数有限的随机变量构成$L_p$空间，记作$L_p(\Omega, \mathbb{F}, P)$。
容易验证，$L_p$空间是线性空间。特别地，$L_2$空间中可定义内积$<X_1, X_2> = \mathbb{E}[X_1 X_2]$，成为内积空间，内积空间的好处是可以定义垂直与投影，我们将看到，条件期望对应的正是$L_2$空间中的投影。

### 条件期望

条件期望$\mathbb{E}(X\mid \mathcal{G})$是定义在$(\Omega, \mathcal{G}, P)$上的随机变量，其中$\mathcal{G} \subset \mathcal{F}$，且$\mathcal{G}$是$\sigma$-代数。考虑$L_2$空间中的随机变量，根据全期望公式，

$$
\begin{aligned}
&\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X\mid \mathcal{G}]] \\
\iff &\int_{\mathcal{G}} X \text{d}P = \int_{\mathcal{G}} \mathbb{E}[X\mid \mathcal{G}] I_A \text{d}P \\
\iff &\int_{A} X I_A \text{d}P = \int_{A} \mathbb{E}[X\mid \mathcal{G}] I_A \text{d}P \\
\iff &<X, I_A> = <\mathbb{E}[X\mid \mathcal{G}], I_A>,
\end{aligned}
$$

其中$I_A \in \mathcal{G}$。可见，$\mathbb{E}(X\mid \mathcal{G})$正是$X$在线性子空间$\mathcal{G}$上的投影。
注意由投影演化出的结论只对$L_2$空间中的随机变量成立。
但$L_2$空间是$L_1$空间的子空间，因为分$X< 1$和$X\ge 1$讨论，可由$\mathbb{E}[X^2]$存在推出$\mathbb{E}[X]$存在。
根据泛函分析可知，可进一步推出投影演化出的结论对$L_1$空间中的随机变量同样成立。

条件期望的塔性质（tower property）是指，对于
$\mathcal{G}_1 \subset \mathcal{G}_2 \subset \mathcal{F}$
，有
$$\mathbb{E}\left[\mathbb{E}\left[X \mid \mathcal{G}_{1}\right] \mid \mathcal{G}_{2}\right]=\mathbb{E}\left[X \mid \mathcal{G}_{1}\right]$$
和
$$\mathbb{E}\left[\mathbb{E}\left[X \mid \mathcal{G}_{2}\right] \mid \mathcal{G}_{1}\right]=\mathbb{E}\left[X \mid \mathcal{G}_{1}\right]$$
。从投影的角度看，说的是多次投影等价于在最小的子空间上一次投影，这与立体几何中的三垂直定理异曲同工。

## 结语

本文简单地介绍了测度论、实分析和高等概率论的基本概念。可以看到，实分析和高等概率论共同的基础是测度论，测度论在实数集上发展为实分析，在全集测度为1的约束下发展为概率论。

这篇介绍涉及到代数、分析、几何、概率论等各数学分支，显示了数学各分支间边界的模糊。事实上，数学是一门贯通的学科，分为各个分支只是为了学习的方便。
