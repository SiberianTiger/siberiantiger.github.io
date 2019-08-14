---
layout: post
title:  "Matrix Norms and Derivatives"
date:   2019-07-27 23:42:00 +0800
author: Siberian Tiger
categories: math
---

## Matrix Norms

Matrix norm is a norm on the vector space $\mathbb{F}^{m \times n}$, where $\mathbb{F} = \mathbb{R}$ or $\mathbb{C}$ denotes the field. Thus, it is a mapping from the vector space to $\mathbb{R}$ which satisfies the following properties of norms:

For all scalars $\alpha \in \mathbb{F}$ and for all matrices $\boldsymbol{A}, \boldsymbol{B} \in \mathbb{F}^{m \times n}$, a norm

- is absolutely homogeneous: $\lVert\alpha\boldsymbol{A}\rVert = \lvert\alpha\rvert \lVert\boldsymbol{A}\rVert$;

- is sub-additive or satisfies the *triangle inequality*: $\lVert\boldsymbol{A} + \boldsymbol{B}\rVert \le \lVert\boldsymbol{A}\rVert + \lVert\boldsymbol{B}\rVert$;

- and is positive-definite: $\lVert\boldsymbol{A}\rVert \ge 0$, and $\lVert\boldsymbol{A}\rVert = 0$ iff $\boldsymbol{A} = \boldsymbol{0}$.

There are several types of matrix norms that satisfy the properties above, and we name a few as follows.

### Induced by Vector Norms

The most general vector-induced $(p, q)$-norm of an $m \times n$ matrix $\boldsymbol{A}$ is defined as 

$$
\|A\|_{p, q}=\sup _{x \neq 0}\left\{\frac{\|A x\|_{q}}{\|x\|_{p}}\right\},
$$
            
where $\|\|_p$ and $\|\|_q$ are vector norms. When $q = p$, the resulting matrix norm is called $\ell_p$ norm for simplicity.

Three noteworthy and widely-used examples are $p = 1, 2$ and $\infty$.

- $p = 1$: $\lVert\boldsymbol{A}\rVert_1 = \max_j \sum_i \lvert a_{ij}\rvert$, which is the maximum absolute column sum.

- $p = \infty$: $\lVert\boldsymbol{A}\rVert_\infty = \max_i \sum_j \lvert a_{ij}\rvert$, which is the maximum absolute row sum.

- $p = 2$: $\lVert\boldsymbol{A}\rVert_2 = \sigma_{\max} \boldsymbol{A}$, which is the largest singular value.

### Entrywise

The most famous entrywise matrix norm is the Frobenius norm: $\lVert\boldsymbol{A}\rVert_F = (\sum_i \sum_j \lvert a_{ij}\rvert^2)^{1/2}$. An important inequality relating $\ell_2$ norm to the Frobenius norm states that $\lVert\boldsymbol{A}\rVert_2 \le \lVert\boldsymbol{A}\rVert_F$.

### References

- Wikipedia: <https://en.wikipedia.org/wiki/Matrix_norm>.

## Matrix derivatives

We first introduce some direct extensions of scalar derivative.

$$
\frac{\partial \boldsymbol{f}}{\partial x}=\left[\begin{array}{c}{\frac{\partial f_{1}}{\partial x}} \\ {\frac{\partial f_{2}}{\partial x}} \\ {\vdots} \\ {\frac{\partial f_{n}}{\partial x}}\end{array}\right], \quad 
\frac{\partial f}{\partial \boldsymbol{x}}=\left[\begin{array}{c}{\frac{\partial f}{\partial x_{1}}} \\ {\frac{\partial f}{\partial x_{2}}} \\ {\vdots} \\ {\frac{\partial f}{\partial x_{n}}}\end{array}\right].
$$

Then, following the right-side formula above, we
have 

$$
\frac{\partial \boldsymbol{f}^{\top} \boldsymbol{g}}{\partial \boldsymbol{x}}=\frac{\partial \boldsymbol{f}^{\top}}{\partial \boldsymbol{x}} \cdot \boldsymbol{g}+\frac{\partial \boldsymbol{g}^{\top}}{\partial \boldsymbol{x}} \cdot \boldsymbol{f} \in \mathbb{R}^{n},
$$

where $\boldsymbol{f}, \boldsymbol{g} \in \mathbb{R}^{m}, \boldsymbol{x} \in \mathbb{R}^n$. This has used the definition 

$$
\frac{\partial \boldsymbol{f}^{\top}}{\partial \boldsymbol{x}}=\left[\begin{array}{cccc}{\frac{\partial f_{1}}{\partial x_{1}}} & {\frac{\partial f_{2}}{\partial x_{1}}} & {\cdots} & {\frac{\partial f_{m}}{\partial x_{1}}} \\ {\frac{\partial f_{1}}{\partial x_{2}}} & {\frac{\partial f_{2}}{\partial x_{2}}} & {\dots} & {\frac{\partial f_{m}}{\partial x_{2}}} \\ {\vdots} & {\vdots} & {\ddots} & {\vdots} \\ {\frac{\partial f_{1}}{\partial x_{n}}} & {\frac{\partial f_{2}}{\partial x_{n}}} & {\cdots} & {\frac{\partial f_{m}}{\partial x_{n}}}\end{array}\right]_{n \times m}.
$$

It is weird that some materials directly define 

$$
\left(\frac{\partial f}{\partial x}\right)_{i, j}=\frac{\partial f_{i}}{\partial x_{j}}.
$$

The right way is to define 

$$
\left(\frac{\partial \boldsymbol{f}^{\top}}{\partial \boldsymbol{x}}\right)_{i, j}=\frac{\partial f_{j}}{\partial x_{i}}, \quad
\left(\frac{\partial \boldsymbol{f}}{\partial \boldsymbol{x}^{\top}}\right)_{i, j}=\frac{\partial f_{i}}{\partial x_{j}}.
$$

Also, the notation of taking the derivative of a matrix w.r.t. a vector
like $\frac{\partial \boldsymbol{A}}{\partial \boldsymbol{x}}$ is weird. I don’t understand
why it keeps showing up in different materials.

### References

- Wikipedia: <https://en.wikipedia.org/wiki/Matrix_calculus>.

- Appendix C of Pattern Recognition and Machine Learning.

- Lecture notes of Introduction to System Engineering, Prof. Jianming Hu, Department of Automation, Tsinghua University, Spring 2018.
