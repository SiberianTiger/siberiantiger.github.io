---
layout: post
title:  "MIT 6.436 Fundamentals of Probability Lecture Notes"
date:   2019-10-21 01:30:00 -0500
author: Siberian Tiger
categories: math
---

## Index

- [Index](#index)
- [Lecture 1](#lecture-1)
  - [Introduction](#introduction)
  - [Probability space](#probability-space)
  - [Sample space](#sample-space)
  - [Discrete probability space](#discrete-probability-space)
  - [$\sigma$-field](#sigma-field)
    - [Intersection of $\sigma$-fields](#intersection-of-sigma-fields)
    - [Borel $\sigma$-field](#borel-sigma-field)
  - [Measure and probability](#measure-and-probability)
- [Lecture 2](#lecture-2)
  - [Measure and probability](#measure-and-probability-1)
  - [Continuity of probability measures](#continuity-of-probability-measures)
  - [Caratheodory's extension theorem and the extension to a probability space](#caratheodorys-extension-theorem-and-the-extension-to-a-probability-space)
    - [Uniform measure on $[0, 1]$](#uniform-measure-on-0-1)
- [Lecture 3](#lecture-3)
  - [Caratheodory's extension theorem and the extension to a probability space](#caratheodorys-extension-theorem-and-the-extension-to-a-probability-space-1)
    - [Uniform measure on $\{0, 1\}^{\infty}$](#uniform-measure-on-0-1infty)
  - [Conditional probability](#conditional-probability)
  - [Independence](#independence)
  - [Borel-Cantelli lemma](#borel-cantelli-lemma)
- [Lecture 4](#lecture-4)
  - [Borel-Cantelli lemma](#borel-cantelli-lemma-1)
  - [Preliminaries of combinatorial probability](#preliminaries-of-combinatorial-probability)
    - [$e$ as a limit](#e-as-a-limit)
    - [Stirling's formula](#stirlings-formula)
    - [Permutations](#permutations)
  - [Combinatorial probability](#combinatorial-probability)
    - [Mafia game](#mafia-game)
    - [Ordered lists and unordered lists](#ordered-lists-and-unordered-lists)
    - [Birthday paradox](#birthday-paradox)
    - [Coupon collection problem](#coupon-collection-problem)
- [Lecture 5](#lecture-5)
  - [Combinatorial probability](#combinatorial-probability-1)
    - [Coupon collection problem](#coupon-collection-problem-1)
  - [Random variables](#random-variables)
    - [Measurable functions](#measurable-functions)
  - [Cumulative distribution functions](#cumulative-distribution-functions)
- [Lecture 6](#lecture-6)
  - [Cumulative distribution functions](#cumulative-distribution-functions-1)
  - [Independence of random variables](#independence-of-random-variables)
  - [Continuous random variables](#continuous-random-variables)
  - [Review of infinite integrals](#review-of-infinite-integrals)
  - [Discrete random variables](#discrete-random-variables)
  - [Expectation and its properties](#expectation-and-its-properties)
- [Lecture 7](#lecture-7)
  - [Expectation and its properties](#expectation-and-its-properties-1)
    - [Properties of expectation](#properties-of-expectation)
    - [Comments on expectation](#comments-on-expectation)
    - [Expectation of some discrete distributions](#expectation-of-some-discrete-distributions)
  - [Covariance and correlation coefficient](#covariance-and-correlation-coefficient)
  - [Indicator random variables](#indicator-random-variables)
- [Lecture 8](#lecture-8)
  - [Memoryless distributions](#memoryless-distributions)
  - [Gaussian distributions](#gaussian-distributions)
    - [Tails](#tails)
  - [Expectations of a continuous random variable](#expectations-of-a-continuous-random-variable)
    - [Properties of expectations](#properties-of-expectations)
- [Lecture 9](#lecture-9)
  - [Joint density and jointly continuous random variables](#joint-density-and-jointly-continuous-random-variables)
  - [Conditional probability density functions](#conditional-probability-density-functions)
  - [Bivariate normal random variables](#bivariate-normal-random-variables)
  - [Conditional expectation](#conditional-expectation)
- [Lecture 10](#lecture-10)
  - [Conditional expectation](#conditional-expectation-1)
  - [Derived distributions](#derived-distributions)
  - [Bivariate normal in polar coordinates](#bivariate-normal-in-polar-coordinates)
- [Lecture 11](#lecture-11)
  - [Sum of two independent random variables](#sum-of-two-independent-random-variables)
  - [Lebesgue integral and expectation of a general random variable](#lebesgue-integral-and-expectation-of-a-general-random-variable)
  - [Monotone convergence theorem](#monotone-convergence-theorem)
- [Lecture 12](#lecture-12)
  - [Monotone convergence theorem](#monotone-convergence-theorem-1)
    - [Application of MCT: Approximating $g$ from below using special simple functions](#application-of-mct-approximating-g-from-below-using-special-simple-functions)
    - [Application of MCT: Proof of linearity of Lebesgue integral](#application-of-mct-proof-of-linearity-of-lebesgue-integral)
    - [Application of MCT: Proof of Boral-Cantelli lemma](#application-of-mct-proof-of-boral-cantelli-lemma)
  - [Fatou's lemma](#fatous-lemma)

## Lecture 1

> David Gamarnik  
> Wed, Sep 4, 2019

### Introduction

The course Fundamentals of Probability is given by Prof. David GAMARNIK from Sloan, with the TA Eren Kizildag from EECS. In this semester, we will change our course website from Stella to Canvas, where I have posted the syllabus.

A real analysis background helps in this course, but is not necessary. At least you should be familar with notations like $\limsup$ and $\liminf$. Refer to wiki if you are not familiar with the two notations.

This course is graded by three parts: 
- the weekly homework takes up 30%, 
- the midterm exam takes 2 hours and accounts for 30% and 
- the final exam takes 3 hours and accounts for 40%.

This course covers three topics:
- Measure Theory Foundations. Learning measure theory is like learning words before making sentences.
- Laws of Probability. Including Laws of Large Numbers and Central Limit Theorems.
- Stochastic Processes. Like Poisson processes, Markov chains and martingales.

### Probability space

Probability is about quantifying uncertainty. To this end, a triple $(\Omega, \mathcal{F}, \mathbb{P})$ called probability space is needed, where $\Omega$ is a sample space, $\mathcal{F}$ is a $\sigma$-field, and $\mathbb{P}$ is a probability measure. Now we look at them in details.

### Sample space

A **sample space** $\Omega$ is an arbitrary set. It can be 
- finite, e.g. $\{1, 2, \cdots, n\}$,
- countable, e.g. $\{a_1, a_2, \cdots, a_n, \cdots\}$, $\mathbb{Z}$ (integers), $\mathbb{Q}$ (rational numbers), or 
- uncountable, $\{0, 1\}^{\infty}$ (set of all infinite sequences of zeros and ones). 

Elements of the sample space are called **elementary outcomes** and denoted by $\omega$.

Here are some examples of sample spaces.

1. Roll a die once. $\Omega = \{1, 2, 3, 4, 5, 6\}$. The $\Omega$ here is finite.
2. Roll a die 10 times. $\Omega = \{1, 2, 3, 4, 5, 6\}^{10} = \{(a_1, \cdots, a_{10}): a_i \in \{1, \cdots, 6\}, i = 1, \cdots, 10\}$. In this case, $(3, 1, 1, 4, 5, 6, 5, 4, 3, 1)$ is an $\omega$. The $\Omega$ here is finite.
3. $\Omega = \mathbb{Z}_{+}$ (non-negative integers). The $\Omega$ here is countable.
4. $\Omega = \{0, 1\}^{\infty}$. This is the sample space of tossing a coin for infinite times. The $Omega$ here is uncountable.

### Discrete probability space

A **discrete probability space** is a $(\Omega, \mathcal{F}, \mathbb{P})$ where 
1. $\Omega$ is finite or countable;
2. $\mathcal{F}$ is the set of all subsets of $\Omega$; let $\lvert\Omega\rvert$ be the cardinality of $\Omega$, then if $\lvert\Omega\rvert < +\infty$, $\lvert\mathcal{F}\rvert = 2^{\lvert\Omega\rvert}$.
3. $\mathbb{P}$ is a function $\Omega \rightarrow [0, 1]$, such that $\sum_{\omega \in \Omega} \mathbb{P}(w) = 1$.

Here, 'discrete' follows the fact that the sample space is finite or countable.

Before proceeding, we borrow some notations from real analysis, $\forall$ for 'for every', $\exists$ for 'exists' and $\triangleq$ for 'equal by definition'.
Then $\forall A \in \mathcal{F}$ (i.e. $\forall A \subset \Omega$), $\mathbb{P}(A) \triangleq \sum_{\omega\in A} \mathbb{P}(\omega)$.

We now give three examples of discrete probability spaces.
1. Toss a fair coin twice. Denote heads by 1 and tails by 0. Then 
   - $\Omega = \{(0, 0), (0, 1), (1, 0), (1, 1)\}$;
   - $\lvert\mathcal{F}\rvert = 2^4 = 16$$;
   - $\mathbb{P}((0, 0)) = \mathbb{P}((0, 1)) = \mathbb{P}((1, 0)) = \mathbb{P}((1, 1)) = 1/4$.
2. $\Omega = \{3, \text{DAVID}, 15.085\}$, each elementary outcome with probability $0.3$, $0.1$ and $0.6$.
3. Poisson discrete probability space. For a fixed $\lambda > 0$, take $\Omega = \mathbb{Z}_{+}$. Then $\mathbb{P}(n) = \frac{\lambda^n}{n!}e^{-\lambda}$. To verify the third condition of discrete probability space, notice that $\sum_{n=0}^{\infty} \mathbb{P}(n) = e^{-\lambda}\sum_{n=0}^{\infty}\frac{\lambda^n}{n!} = e^{-\lambda} \cdot e^{\lambda} = 1$.

### $\sigma$-field

Uncountable sample spaces are common in our lives. For example, the temperature tomorrow, if predicted as at least 70 $^\circ$F and at most 72 $^\circ$F, has an uncountable sample space.

Given $\Omega$, the difficulty of treating uncountable sample spaces lies in the question: *can we associate $\mathbb{P}(A)$ for all $A \subset \Omega$?*

If we want to define $\mathcal{F}$ similarly to the discrete probability space, then what properties should $\mathcal{F}$ satisfy for an uncountable sample space?
We can conjecture a few, like
- the empty set $\emptyset \in \mathcal{F}$;
- $\Omega \in \mathcal{F}$;
- if $A, B \in \mathcal{F}$, then $A \cup B, A \cap B \in \mathcal{F}$ and $A^{c} = \Omega \backslash A \in \mathcal{F}$.

Now we give a formal definition of a $\sigma$-field or $\sigma$-algebra.

Given $\Omega$, a **$\sigma$-field** $\mathcal{F}$ is any set of subsets of $\Omega$, such that 
1. $\emptyset \in \mathcal{F}$ (this ensures that $\mathcal{F} is non-empty);
2. if $A \in \mathcal{F}$, then $A^c \in \mathcal{F}$;
3. if $A_1, A_2, \cdots, A_n, \cdots \in \mathcal{F}$, then $\cup_{n=1}^{\infty} A_n \in \mathcal{F}$. 

By de Morgan's laws, the third condition also has implications for intersection.

We now give some examples of $\sigma$-fields.
1. Given $\Omega$, the simplest $\mathcal{F} = \{\emptyset, \Omega\}$.
2. Given $\Omega = \{1, \cdots, 6\}^{\infty}$, let $A = \{(w_1, w_2, \cdots): 1 \le w_1 \le 2\}, B = \{(w_1, w_2, \cdots): 3 \le w_1 \le 4\}, C = \{(w_1, w_2, \cdots): 5 \le w_1 \le 6\}$. Then $\mathcal{F} = \{\emptyset, A, B, C, A\cup B, B\cup C, A\cup C, A\cup B\cup C\}$. This is our first non-trivial example of $\sigma$-fields. 
3. All subsets of $\Omega$.

#### Intersection of $\sigma$-fields

*Proposition.* Let $\{\mathcal{F}_s\}$ be a set of $\sigma$-fields. Then $\mathcal{F} = \cap_{s} \mathcal{F}_s = \{A\subset \Omega: A \in \mathcal{F}_s, \forall s\}$ is also a $\sigma$-field.

*Proof.*
1. $\emptyset \in \mathcal{F}_s, \forall s \Rightarrow \emptyset \in \mathcal{F}$.
2. Suppose $A \in \mathcal{F} \Rightarrow A \in \mathcal{F}_s, \forall s \Rightarrow A^c \in \mathcal{F}_s, \forall s \Rightarrow A^c \in \mathcal{F}$.
3. Exercise.

#### Borel $\sigma$-field

Take any set $\mathcal{C}$ of subsets of $\Omega$. Define $\sigma(\mathcal{C})$ as the intersection of all $\sigma$-fields containing $\mathcal{C}$.

*Example.* $\Omega = \{1, 2, 3, 4, 5, 6\}$, $\mathcal{C} = \{(1, 2), (3, 4), (5, 6)\}$. Then $\sigma(\mathcal{C}) = \{\emptyset, (1, 2), (3, 4), (5, 6), (1, 2, 3, 4), (3, 4, 5, 6), (1, 2, 5, 6), (1, 2, 3, 4, 5, 6)\}$, similar to the second example of $\sigma$-fields.

Now take $\Omega = [0, 1]$. Let $\mathcal{C}$ be all closed intervals, i.e. $\mathcal{C} = \{[a, b]: 0\le a\le b\le 1\}$. Then $\sigma(\mathcal{C})$ is called **Borel $\sigma$-field**. Note that Borel $\sigma$-field does *not* contain all subsets of $[0, 1]$. 

### Measure and probability

Given $(\Omega, \mathcal{F})$, a **measure** is a function $\mu: \mathcal{F} \rightarrow \mathbb{R}_{+}$, such that
1. $\mu(\emptyset) = 0$;
2. if $\{A_i, i = 1, 2, \cdots\}$ is a countable sequence of *disjoint* elements of $\mathcal{F}$, then $\mu(\cup_{i=1}^{\infty} A_i) = \sum_{i=1}^{\infty}\mu(A_i)$ (sum of numbers). 'Disjoint' means $A_i \cap A_j = \emptyset, \forall i \neq j$.

Measures are a generalization of volumes.

------

## Lecture 2

> David Gamarnik  
> Mon, Sep 9, 2019

### Measure and probability

Measure space with $\mu(\Omega) = 1$. A probability space is denoted by $(\Omega, \mathcal{F}, \mathbb{P})$.

### Continuity of probability measures

Given $(\Omega, \mathcal{F})$, and $\mathbb{P}$ that satisfies finite additivity. Then the following are equivalent.

1. $\mathbb{P}$ is countably additive.
2. For any increasing sequence.
3. For any decreasing sequence.
4. For any decreasing sequence such that $\cap_{n=1}^{\infty} A_n = \emptyset$.

### Caratheodory's extension theorem and the extension to a probability space

*Caratheodory's extension theorem.* 
Given $\Omega$. Suppose $\mathcal{F}_0$ is a field. Suppose $\mathbb{P}_0: \mathcal{F}_0 \mapsto [0, 1]$ such that $\mathbb{P}_0(\Omega) = 1$ and $\mathbb{P}_0$ is countably additive. Then there is a unique extenion of $\mathbb{P}_0$ to $(\Omega, \sigma(\mathcal{F}_0), \mathbb{P})$, such that $\forall A\in \mathcal{F}_0$, $\mathbb{P}(A) = \mathbb{P}_0(A)$.

#### Uniform measure on $[0, 1]$

$(\Omega = (0, 1], \mathcal{B}, \mathbb{P})$

------

## Lecture 3

> David Gamarnik  
> Wed, Sep 11, 2019

### Caratheodory's extension theorem and the extension to a probability space

#### Uniform measure on $\{0, 1\}^{\infty}$

Let $\Omega$ be the sample space of infinite coin tosses.
For all $n$, let $\mathcal{F}$ be all events associated with first $n$ outcomes. $\mathcal{F} _{0} = \bigcup _{n=1} ^{\infty} \mathcal{F} _{n}$, which is a field consisting of all events which can be described by finitely many tosses. We can extend $\mathcal{F} _{0}$ to $\sigma(\mathcal{F} _{0})$ by Caratheodory's extension theorem.

Actually, $\sigma(\mathcal{F}_0) = \mathcal{B}$.

An example that an event that is uncountably infinite has a zero probability.

Definition of 'almost surely', or a.s.

### Conditional probability

*Definition.*

*Theorem.*

1. If $A_i$ disjoint, then $\mathbb{P}\left(\bigcup_{i=1}^{\infty} A_{i} \mid B\right)=\sum_{i=1}^{\infty} \mathbb{P}\left(A_{i} \mid B\right)$.
2. Rule of conditional probability.
3. Bayes' Rule


### Independence

*Definition.* Independence of events $A, B\in \mathcal{F}$.

*Definition.* Independence of $\sigma$-fields $\mathcal{F}_1, \mathcal{F}_2 \subset \mathcal{F}$.

### Borel-Cantelli lemma

*Definition.* $\{A_n, i.o.\} = \cap_{n=1}^{\infty} \cup_{i=n}^{\infty} A_i$. It means events that occurs infinitely often.

*Borel-Cantelli lemma.*  
1. Suppose $\{A_n, n\ge 1\}$ is a sequence of events such that $\sum_{i=1}^{\infty} \mathbb{P}(A_n) < +\infty$, then $\mathbb{P}(A_n, i.o.) = 0$.
2. Suppose $\{A_n, n\ge 1\}$ is a sequence of events such that $\sum_{i=1}^{\infty} \mathbb{P}(A_n) = +\infty$ and $A_n$ are independent, then $\mathbb{P}(A_n, i.o.) = 1$.

------

## Lecture 4

> David Gamarnik  
> Mon, Sep 16, 2019

### Borel-Cantelli lemma

Proof of Borel-Cantelli lemma.

- Use union bounds.
- Use the following lemma. $0 \le p_n \le 1, \forall n \in \mathbb{N}$. Suppose $\sum_{n=1}^{\infty} p_n = +\infty$. Then $\prod_{i=1}^{\infty} (1-p_i) = 0$. The proof of this lemma uses the concavity of $\log(1-x)$.

### Preliminaries of combinatorial probability

#### $e$ as a limit

- $\lim_{n\rightarrow \infty} (1+\frac{1}{n})^n = e$.
- For any $a_n \rightarrow a$, $\frac{b_n}{n} \rightarrow 1$ as $n\rightarrow \infty$, $(1+\frac{a_n}{n})^{b_n} \rightarrow e^a$. (Proof by Taylor approximation)

#### Stirling's formula

$n! \approx \frac{n^{n+\frac{1}{2}}}{e^n}\sqrt{2\pi}$.

#### Permutations

$n!$.

### Combinatorial probability

#### Mafia game

$\mathbb{P}(\text{all die}) = \frac{n!}{n^n} \approx \frac{\sqrt{2\pi n}}{e^n} \rightarrow e^{-n}$.

$\mathbb{P}(\text{member no. 1 survives}) = (\frac{n-1}{n})^n \rightarrow e^{-1}$.

#### Ordered lists and unordered lists

- Given $n$ distinct elements $1, 2, \cdots, n$ and $1\le k\le n$, how many unordered lists of $k$ distinct objects can we create? $\frac{n!}{(n-k)!}$.
- Unordered lists: $\frac{n!}{k!(n-k)!} = {n \choose k}$.

#### Birthday paradox

Let $A$ denote the event that all $n$ students have distinct birthdays. Then $\mathbb{P}(A) = \frac{365!}{(365-n)! \times 365^n}$.

Paradox: $n=23$, $\mathbb{P}(A) \approx \frac{1}{2}$.

#### Coupon collection problem

Let $1, 2, \cdots, n$ denote coupons. At $t = 1, 2, \cdots$ a uniformly random coupon is collected (repitition allowed). How soon till all coupons are collected?

Informally, $T = n \log n$.
Formally, we have the following theorem.

*Theorem.* Let $t = cn\log n$, where $c > 0$. Let $c_1, c_2, \cdots, c_t$ be distinct coupons collected.

- Suppose $c > 1$, then $\lim_{n\rightarrow \infty} \mathbb{P}(\{c_1, \cdots, c_t\} = \{1, \cdots, n\}) = 1$.
- Suppose $c < 1$, then $\lim_{n\rightarrow \infty} \mathbb{P}(\{c_1, \cdots, c_t\} = \{1, \cdots, n\}) = 0$.

------

## Lecture 5

> David Gamarnik  
> Wed, Sep 18, 2019

### Combinatorial probability

#### Coupon collection problem

*Proof* for the *Theorem* when $c > 1$.
- Let $A_t$ denote the event that not all coupon collected up to $t$. It remains to show $\mathbb{P}(A_t) \rightarrow 0$.
- $A_t = \cup_{i=1}^{n} B_{t, i}$, where $B_{t, i}$ denotes that coupon $i$ is not collected.
- Apply union bound, and show $\mathbb{P}(B_{t, i}) \rightarrow 0$ by Taylor approximation.

### Random variables

*Definition.*
Given $(\Omega, \mathcal{F})$, $\forall c \in \mathbb{R}, X^{-1}(c) = \{\omega \in \Omega: X(w) \le c\} \in \mathcal{F}$.

Extended-valued r.v.: $\Omega \rightarrow \mathbb{R}\cup \{+\infty\}$.

Indicator function $I_A$.

Simple random variables.  
*Definition.* (Different from lecture notes) $X: \Omega \rightarrow \mathbb{R}$ is simple if $\lvert\text{Im}(X)\rvert < +\infty$, where $\text{Im}(X)$ is the set of all values realized by $X$. Here $\text{Im}$ denotes the image of a function (image is opposed to preimage).

If $X$ is simple, $X = \sum_{i=1}^m x_i I_{A_i}$.

#### Measurable functions

$(\mathcal{F}_1, \mathcal{F}_2)$-measurable , i.e. generalization of random variables. Given $(\Omega_1, \mathcal{F}_1)$, $(\Omega_2, \mathcal{F}_2)$. $X: \Omega_1 \rightarrow \Omega_2$ is called $(\mathcal{F}_1, \mathcal{F}_2)$-measurable if $\forall B \in \mathcal{F}_2$, $X^{-1}(B) = \{\omega \in \Omega_1: X(\omega) \in B\} \in \mathcal{F}_1$.

A r.v. is a special case with $(\Omega_2, \mathcal{F}_2) = (\mathbb{R}, \mathcal{B})$.

### Cumulative distribution functions

*Definition.* $F_X: \mathbb{R} \rightarrow [0, 1]$ defined by $F_X(x) = \mathbb{P}(X \le x)$.

*Theorem.* Given a r.v. $X$, $F_X$ satisfies
1. monotinicity;
2. $\lim_{x\rightarrow -\infty} F_X(x) = 0$, $\lim_{x\rightarrow +\infty} F_X(x) = 1$;
3. right-continuity, i.e. $\forall x\in \mathbb{R}$, $\lim_{y\downarrow x} F_X(y) = F_X(x)$.

------

## Lecture 6

> David Gamarnik  
> Mon, Sep 23, 2019

### Cumulative distribution functions

Proof of right continuity: $x_n \downarrow x$, $x_n$ decreasing and $\lim_{n\rightarrow \infty} x_n$.

CDF uniquely defines the "distribution" of a r.v.
Given $X, Y$ such that $F_X(t) = F_Y(t), \forall t \in \mathbb{R}$. Then $\forall B \subset \mathbb{R}, B \in \mathcal{B}$, $\mathbb{P}(X\in B) = \mathbb{P}(Y\in B)$.

*Theorem.* For every function $F: \mathbb{R} \mapsto [0, 1]$ which satisfies the three properties of a CDF, $\exists (\Omega, \mathcal{F}, \mathbb{P})$ (not unique) and $X: \Omega \mapsto \mathbb{R}$, such that $F_X = F$.

### Independence of random variables

*Definition.* Let $X_1, \cdots, X_m$ be random variables on the same probability space. They are independent if $\forall B_1, \cdots, B_m \in \mathcal{B}$, 
$$
\mathbb{P}\left(X_{1} \in B_{1}, \ldots, X_{n} \in B_{n}\right)=\mathbb{P}\left(X_{1} \in B_{1}\right) \cdots \mathbb{P}\left(X_{n} \in B_{n}\right).
$$

*Proposition.* $X_1, \cdots, X_m$ are independent iff $\forall x_1, \cdots, x_m \in \mathbb{R}$, 
$$
\mathbb{P}(X_1\le x_1, \cdots, X_m\le x_m) = \prod_{j=1}^m \mathbb{P}(X_j \le x_j) = \prod_{j=1}^{m} F_{X_j}(x_j).
$$

### Continuous random variables

*Definition.* A random variable $X$ is continuous if $\exists f: \mathbb{R}\mapsto \mathbb{R}_{+}$, such that $F_X(x) = \int_{-\infty}^{x} f(t) dt$ (Riemann integral).
$f$ is the probability density function (PDF).

If $f$ is continuous at $x_0$, then $\dot{F}_X(x_0) = f(x_0)$.

### Review of infinite integrals

$f^{+}$, $f^{-}$.

$\int_{-\infty}^{+\infty} f(t) dt = \int_{-\infty}^{+\infty} f^{+}(t) dt - \int_{-\infty}^{+\infty} f^{-}(t) dt$ in all cases except $\int_{-\infty}^{+\infty} f^{+}(t) dt = \int_{-\infty}^{+\infty} f^{-}(t) dt = +\infty$.

### Discrete random variables

*Definition.* $x_1, x_2, \cdots, x_m, \cdots$. $\mathbb{P}(X = x_m) = p_m$. 
$p_X(x) = \mathbb{P}(X = x)$ is the probability mass function (PMF).

*Definition.* (Joint PMF)  
Given $X_1, \cdots, X_m: \Omega \mapsto \mathbb{R}$ are discrete random variables, their joint PMF 
$$
p_{X_1, \cdots, X_m}(x_1, \cdots, x_m) = \mathbb{P}(X_1 = x_1, \cdots, X_m = x_m).
$$

*Definition.* (Independence of discrete r.v.)  
$X \perp Y$ iff $\forall x, y$, $\mathbb{P} _{X, Y}(x, y) = p _{X}(x) p_Y(y)$.

### Expectation and its properties

*Definition.* Discrete random variable $X$

*Power law.* Fix $\alpha > 0$. $p_{X}(k) = 1/k^{\alpha} - 1/(k+1)^{\alpha}, \forall k \in \mathbb{N}$.
$$
\mathbb{E}[X] = \sum_{n=1}^{+\infty} \mathbb{P}(X\ge n) = \sum_{n=1}^{+\infty} \frac{1}{n^\alpha} = \zeta(\alpha),
$$
which is the Riemann zeta function. $\zeta(\alpha) < +\infty$ iff $\alpha > 1$.

------

## Lecture 7

> Eren Kizildag  
> Wed, Sep 25, 2019

### Expectation and its properties

Discrete r.v. $X$. 

*Fact.* 
$\mathbb{E}[X] = \sum_{n\ge 0}[X\ge n] = \sum_{n\ge 1}[X\ge n]$.

*Theorem.* 
$\mathbb{E}[g(X)] = \sum_{x: p_X(x) \ge 0} g(X) p_{X}(x)$.

*Definitions.*
1. $\mathbb{E}[X^k]$: $k$-th moment.
2. $\mathbb{E}[(X - \mathbb{E}[X])^k]$: $k$-th central moment.
3. Variance is second central moment.
4. Standard deviation is $\sqrt{\operatorname{VAR}(X)}$.

$X \ge 0$ a.s. $\iff$ $\mathbb{P}(\{\omega: X(\omega)\ge 0\}) = 1$.

#### Properties of expectation

1. If $X\ge 0$ a.s., then $\mathbb{E}[X] \ge 0$.
2. If $X = c$ a.s., then $\mathbb{E}[X] = c$.
3. Linearity of expectation.  
   The proof.
4. If $\mathbb{E}[X] < \infty$, then $\operatorname{VAR}[X] = \mathbb{E}[X^2] - (\mathbb{E}[X])^2$.
5. $\operatorname{VAR}[aX] = a^2 \operatorname{VAR}[X], \forall a\in \mathbb{R}$.
6. If $X, Y$ are independent, then
   - $\mathbb{E}[XY] = \mathbb{E}[X] \mathbb{E}[Y]$;
   - $\operatorname{VAR}[X+Y] = \operatorname{VAR}[X] + \operatorname{VAR}[Y]$.  
     The proof.  
     If $X, Y$ are independentm, then $\mathbb{E}[g(X)\cdot h(Y)] = \mathbb{E}[g(X)]\cdot \mathbb{E}[h(Y)]$.

#### Comments on expectation

1. $\mathbb{E}[X]$ is well defined if $\sum_{x > 0} x p_X(x)$ and $\sum_{x < 0} x p_X(x)$ are not both infinite.  
   Moreover, $\mathbb{E}[X] < \infty$ if both sums above are finite.
2. $\mathbb{E}[\lvert X\rvert] = \mathbb{E}[X^{+}] + \mathbb{E}[X^{-}]$. If $\mathbb{E}[\lvert X\rvert] < \infty$, then $X$ is **integrable**. 
3. $\mathbb{E}[X^2]$ is always well defined. If $\mathbb{E}[X^2] < \infty$, then $X$ is **square integrable**.  
   If a r.v. is square integrable, then it is necessarily integrable, because $|X|^2 + 1 \ge 2|X| \ge |X|$.
4. Let $r > 0$. If $\mathbb{E}[\lvert X\rvert^r] < \infty$, then $\mathbb{E}[\lvert X\rvert^k] < \infty$ for every $0 < k \le r$.
5. $\operatorname{VAR}[X]$ is
   - $< \infty$, if $X$ is square integrable;
   - $= \infty$, if $X$ is integrable but not square integrable;
   - undefined, if $X$ is not integrable.

#### Expectation of some discrete distributions

Expected value of Geometry distribution: $\mathbb{E}[X] = 1/p$.

Expected value of Poisson distribution: $\mathbb{E}[X] = \lambda$ (rate).

Binomial distribution becomes Poisson distribution when $n\rightarrow \infty$ and $p = \lambda / n \rightarrow 0$.

### Covariance and correlation coefficient

$\operatorname{Cov}(X, Y) = \mathbb{E}[\widetilde{X} \widetilde{Y}]$, where $\widetilde{X} = X - \mathbb{E}[X]$ and $\widetilde{Y} = Y - \mathbb{E}[Y]$.

It turns out that $X, Y$ are both square integrable, then the Cov is well-defined, since $\lvert \widetilde{X}\widetilde{Y}\rvert \le (\widetilde{X}^2 + \widetilde{Y}^2) / 2$.

*Properties.*
1. $\operatorname{Cov}(X, X) = \operatorname{Var}(X)$.
2. Translation invariant.
3. Commutative.
4. Bilinear.

$\operatorname{Cov}(X, Y) = \mathbb{E}[XY] - \mathbb{E}[X]\cdot \mathbb{E}[Y]$.

If $X \perp Y$, then $\operatorname{Cov}(X, Y) = 0$. The opposite direction is not true.  
An example.

Correlation coefficient 
$$
p(X, Y) = \frac{\operatorname{Cov}(X, Y)}{\sqrt{\operatorname{VAR}(X)\operatorname{VAR}(Y)}}.
$$

1. $-1 \le p(X, Y) \le 1$
2. $p = 1$ if $Y - \mathbb{E}[Y] = a (X - \mathbb{E}[X])$ for some $a > 0$. $p = -1$ if ...

This first property is proved by Cauchy-Schwarz inequality $(\mathbb{E}[XY])^2 \le \mathbb{E}[X^2]\cdot \mathbb{E}[Y^2]$.  
Proof using $\mathbb{E}[(X-tY)^2] \ge 0$.

### Indicator random variables

*Definition.*
$I_A: \Omega \mapsto \{0, 1\}$.

- $I_{A^c} = 1 - I_A$.
- $I_{A\cap B} = I_A \cdot I_B$.

Indicator r.v. can be used to prove $\mathbb{P}(A\cup B) = \mathbb{P}[A] + \mathbb{P}[B] - \mathbb{P}[A\cap B]$.

------

## Lecture 8

> David Gamarnik  
> Mon, Sep 30, 2019

### Memoryless distributions

Review: Continuous random variables

*Definition.*

*Comment.*  
- If $f$ is a PDF, $E = \{t: f(t) < 0\}$, $\mu(E) = 0$ (Lebesgue measure).
- $X$ continuous $\nRightarrow$ $f$ continuous.

Exponential distributions are the **only** memoryless distributions.

*Definition.*
Fix $\lambda > 0$, $F_X(t) = 1 - e^{-\lambda t}, t\ge 0$, $F_X(t) = 0, t < 0$.

*Memoryless property.*
$\forall x, y \ge 0$, $\mathbb{P}(X - x \ge y \mid X \ge x) = \mathbb{P}(X \ge y)$.

Applications in stochastic processes, queueing and physics.

### Gaussian distributions

*Definition.*
$N(\mu, \sigma^2)$

Standard normal.

#### Tails

Tail: $\mathbb{P}(X \ge t)$. It is the rate of decay as $t\rightarrow \infty$.

- Exponential distribution: $\mathbb{P}(X \ge t) = e^{-\lambda t} = e^{-\Theta(t)}$.
- Gaussian distribution: $\mathbb{P}(X \ge t) \approx e^{-\Theta(t^2)}$.  
  Sub-gaussian.
- Power law distribution (heavy tail): Fix $\alpha > 0$, $c > 0$, $\mathbb{P}(X\ge t) = \frac{c^{\alpha}}{t^{\alpha}}$.

### Expectations of a continuous random variable

*Definition.*

#### Properties of expectations

Linearity.

*Proposition.*
Suppose $X\ge 0$ is a continuous random variable, i.e. $\mathbb{P}(X\ge 0) = 1$, i.e. $\{\omega: X(\omega)\ge 0\}$ a.s. Let $f_X$ be its PDF. Then $\mathbb{E}[X] = \int_{0}^{\infty} \mathbb{P}(X > t) dt$.

$\mathbb{E}[g(X) = \int_{-\infty}^{+\infty} g(t) f_X(t) dt$.

------

## Lecture 9

> David Gamarnik  
> Wed, Oct 2, 2019

### Joint density and jointly continuous random variables

*Definition of jointly continuous.*
$\exists f_{X, Y}: \mathbb{R}^2 \mapsto \mathbb{R}$

- $X, Y$ can be both continuous, but not jointly continuous.  
  *Example.* $X \stackrel{d}{=} U[0, 1]$, $Y = X$.
- $X, Y$ are jointly continuous $\Rightarrow$ $X, Y$ are continuous.  
  $f_X(x) = $  
  $f_Y(y) = $

$X, Y$ are jointly continuous. $X\perp Y$ iff $f_{X, Y} = f_X(x)\cdot f_Y(y)$.

Generalization of continuous random variables w.r.t. Lebesgue integral.  
$\mathbb{P}(X\le x) = \int_{(-\infty, x)} f d\mu$.

### Conditional probability density functions

*Definition.*  
- Conditional CDF $F_{X\mid Y}(x\mid y)$.  
- Conditional PDF $f_{X\mid Y}(x\mid y) = \frac{f_{X, Y}(x, y)}{f_Y(y)}$.

*Fact.*
$\forall y$, $G(x) = F_{X\mid Y}(x\mid y)$ is a CDF (4 properties).

### Bivariate normal random variables

*Definition of jointly normal random variables.*
$X = (X_1, \cdots, X_m)$. $\forall w\in \mathbb{R}^m$, $<w, X> = \sum_{i=1}^{m}w_i X_i$ is normal.

Note that **being jointly normal does not require being jointly continuous**.

Bivariate normal: $m = 2$. Here we define it in another way.

*Definition of bivariate normal random variables.*
Fix $\rho \in (-1, 1)$. Let 
$$
f(x, y) = \frac{1}{2\pi \sqrt{1-\rho^2}} \exp\left(-\frac{x^2 - 2\rho x y + y^2}{2(1 - \rho^2)}\right).
$$

*Proposition.*
1. $f$ is a joint density function.
2. The marginal density of $X$ and $Y$ is $N(0, 1)$.
3. Correlation of $X$ and $Y$ is $\rho(X, Y) = \rho$.
4. Conditional PDF of $X$ given $Y = y$ is $N(\rho y, 1 - \rho^2)$.

*Corollary.*
Bivariate random variables $X$ and $Y$ are independent iff $\rho = 0$.

*Example.*
- $X, Y$ are both normal but not jointly normal.
- $\rho(X, Y) = 0$ yet $X \not\perp Y$.

### Conditional expectation

Discrete $X$ takes $0, 1, \cdots$.
$\mathbb{E}[X\mid Y = y] = \sum_{x = 0}^{\infty} x p_{X\mid Y}(x, y)$.

$\mathbb{E}[X\mid Y]$ is a random variable, 
- (discrete) which takes value $\mathbb{E}[X\mid Y = y]$ with probability $\mathbb{P}(Y = y)$.
- (continuous) which takes value $\mathbb{E}[X\mid Y = y]$ with density $f_{Y}(y)$.

------

## Lecture 10

> David Gamarnik  
> Mon, Oct 7, 2019

### Conditional expectation

*Tower property of conditional probability.*
$\mathbb{E}[\mathbb{E}[X\mid Y] g(Y)] = \mathbb{E}[X g(Y)]$.

*Theorem.*
$\mathbb{E}[X^2] < +\infty$. For every (measurable) $g: \mathbb{R} \rightarrow \mathbb{R}$, 
$$
\mathbb{E}[(X - \mathbb{E}[X\mid Y])^2] \le \mathbb{E}[(X - g(Y))^2].
$$

This theorem means that $\mathbb{E}[X\mid Y]$ is the one that minimizes the difference between $X$ and $g(Y)$. In other words, $\mathbb{E}[X\mid Y]$ is best guess of $X$ given $Y$.

### Derived distributions

Let $X$ be a random vector, i.e. $X = (X_1, \cdots, X_n) \in \mathbb{R}^n$. $X_i$ are jointly continuous. $f_X(x)$ is known for $x \in \mathbb{R}^n$. Let $g: \mathbb{R}^n \mapsto \mathbb{R}^n$. 
**Note** that even if $X$ is continuous, $g(X)$ need not be so.  
Question: what is the density of $Y = g(X)$?

Recall that Jacobian matrix $J(x)$ is the matrix of partial derivatives, where the $(i, j)$-th element is $\partial g_j(x) / \partial x_i$.

*Theorem.*
Under necessary assumptions, $Y = g(X)$ is a continuous random vector with density 
$$
f_Y(y) = f_X(g^{-1}(y)) |J(y)|,
$$
where $J(y)$ is the Jacobian of $g^{-1}$ at $y$, and $|M| = |\det M|$.

*Example.* $X \in \mathbb{R}$. $Y = g(X) = X^3$.

*Example.* $X \in \mathbb{R}$. $Y = g(X) = -X^3$.

In general, for a continuous random variable $X \in \mathbb{R}$, if $g$ is strictly monotonic, i.e. strictly increasing or decreasing, then 
$$
f_Y(y) = f_X(g^{-1}(y)) \frac{1}{|\dot{g}(g^{-1}y)|} = f_X(g^{-1}(y)) \left|\frac{dg^{-1}(y)}{dy}\right|.
$$

*Example.* $X \in \mathbb{R}^n$. $Y = g(X) = MX$, where $M$ is an $n \times n$ matrix. Then $f_Y(y) = f_X(M^{-1}y) / \lvert\det M\rvert = f_X(M^{-1} y) \cdot \lvert\det(M^{-1})\rvert$.

To show this, we need some linear algebra. Fix $x_0 = (x^0_1, \cdots, x^0_n) \in \mathbb{R}^n$, $\delta > 0$. Then $C = \prod_i [X^0_i, X^0_i + \delta]$ is a cube. $D = MC$ maps parallel lines in $C$ to parallel lines in $D$. We have $\operatorname{Vol}(D) = \operatorname{Vol}(C) \lvert\det M\rvert = \delta^n \lvert\det M\rvert$.

### Bivariate normal in polar coordinates

$X \perp Y \stackrel{d}{=} N(0, 1)$. Our goal is to derive the joint density of $(R, \Theta)$ is polar coordinates.

$g: (X, Y) \mapsto (R, \Theta)$. Then $g^{-1}(r, \theta) = (r\cos(\theta), r\sin(\theta))$. $|J_{g^{-1}}| = r$.
Therefore, 
$$
\begin{aligned}
f_{R, \Theta}(r, \theta) &= \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{r^2 \cos^2(\theta)}{2}]\right) \frac{1}{\sqrt{2\pi}} \exp\left(-\frac{r^2 \sin^2(\theta)}{2}\right) r \\
&= \frac{r}{2\pi} \exp\left( -\frac{r^2}{2} \right),
\end{aligned}
$$
where $r \ge 0$, $\theta \in [0, 2\pi]$.

Therefore, $f_{R, \Theta}(r, \theta) = f_R(r) f_{\Theta}(\theta)$, which means $R \perp \Theta$. $Theta$ obeys the uniform distribution on $[0, 2\pi]$. Let $Z = R^2$. Then $f_Z(z) = 1/2 \exp(-z/2) \stackrel{d}{=} \operatorname{Exp}(1/2)$.

The PDF in polar coordinates can be used to show that the constant of a standard normal distribution is $C = 1/\sqrt{2\pi}$.

------

## Lecture 11

> David Gamarnik  
> Wed, Oct 9, 2019

### Sum of two independent random variables

*Convolution formula.*
Given continuous r.v. $X, Y$, with $f_X$, $f_Y$, $X\perp Y$. Then $X + Y$ is a continuous random variable and 
$$
f_{X + Y}(z) = \int_{-\infty}^{+\infty} f_X(z) f_Y(z - t) dt.
$$

*Proof.*
1. Consider $g: (x, y) \mapsto (x + y, y)$, and use derived distribution.
2. Take marginal density.

### Lebesgue integral and expectation of a general random variable

Our goal is to unite the definition of expectation of discrete and continuous r.v. That is to define $\mathbb{E}[X]$ for any r.v. $X: \Omega \mapsto \mathbb{R}$.

*Definition.* 
Let $S(g)$ by the set of all (measurable) simple functions $q$ that are dominated by $g$, i.e.
1. $q\ge 0$ a.s.
2. $q\le g$ a.s. (this requires that $g$ is measurable)

*Definition.*
Given $g: \Omega \mapsto \mathbb{R}$, $g\ge 0$ a.s. Then $\int g d\mu = \sup_{q\in S(g)} \int q d\mu$.

Properties.
1. $g \le h$ a.s. Then $\int g d\mu \le \int h d\mu$.
2. Suppose $g\ge 0$ a.s. and $\int g d\mu = 0$. Then $g = 0$ a.s.
3. Linearity.

### Monotone convergence theorem

$0 \le g_n \le g$ a.s. such that $g_n \uparrow g$ a.s.
Then $\int g_n d\mu \uparrow \int g d\mu$.

*Proof (part 1.1).*  
Suppose $g = q$ is simple and $\int q d\mu = +\infty$.

------

## Lecture 12

> David Gamarnik  
> Wed, Oct 16, 2019

### Monotone convergence theorem

*Proof (part 1.2).*  
Suppose $g = q = \sum_{i=1}^{m} a_i 1 _{A_i}$ is simple and $\int q d\mu < +\infty$.
Let $S = \{i: a_i > 0\}$, $A = \bigcup _{i \in S} A_i$, $B_n = \{\omega\in A: g_n(\omega) \ge q(\omega) - 1/r\}$, where $0 < 1/r < \min_i a_i$.

Then $\int g_n d\mu + \int 1/r 1 _{B_n} d\mu \ge \int q 1 _{B_n} d\mu$. Eventually, show that $\lim _{n\rightarrow \infty} \int g_n d\mu \ge \int q d\mu$.  
On the other hand, $\lim _{n\rightarrow \infty} \int g_n d\mu \le \int q d\mu$, which concludes the proof.

*Proof (part 2).*  
For a general $g$, recall $\int g d\mu = \sup_{q\in S(g)} \int q d\mu$. Let $h_n = \min\{g_n, q\}$. Then $h_n \uparrow q$ a.s. By MCT, 
$\int q d\mu = \lim_{n\rightarrow \infty} \int \min\{g_n, q\} d\mu \le \lim_{n\rightarrow \infty} \int g_n d\mu$.  
Therefore, 
$\lim_{n\rightarrow \infty} \int g_n d\mu \ge \sup_{q \in S(g)} \int q d\mu = \int g d\mu$.  
On the other hand, $\lim_{n\rightarrow \infty} \int g_n d\mu \le \int q d\mu$, which concludes the proof.

Note that in general, $X_n \rightarrow X$ a.s. cannot give $\mathbb{E}X_n \rightarrow \mathbb{E}X$.

*Example.* $U$ uniform at random from $[0, 1]$.
Let $X(u) = n$ if $u \in [0, 1/n]$ and $X(u) = 0$ otherwise. 
$X_n \rightarrow 0$ a.s. 
However, $\mathbb{E}X_n \not\rightarrow \mathbb{E}0 = 0$.

#### Application of MCT: Approximating $g$ from below using special simple functions

For $r \in \mathbb{N}$, define $g_r(w) = i/(2^r)$ if $g(w) < r$ and $g(w) \in [i \in 2^r, (i + 1) / 2^r]$, and $g_r(w) = r if $g(w) \ge r$.

$g_r$ is simple, and $g_r \uparrow g$. By MCT, $\int g_r d\mu \rightarrow \int g d\mu$.

#### Application of MCT: Proof of linearity of Lebesgue integral

*Proof.*
Construct $g_n \in S(g)$ such that $g_n \uparrow g$ a.s., $h_n \in S(h)$ such that $h_n \uparrow h$ a.s.

#### Application of MCT: Proof of Boral-Cantelli lemma

*Proof.*
Let $X_n = 1 _{A_n}$. Show that $\mathbb{E}[\sum _{n=1}^{\infty} X_n] < + \infty$, i.e. $\sum _{n=1}^{\infty} X_n < +\infty$ a.s.

### Fatou's lemma

Let $Y$ be a random variable such that $\mathbb{E}|Y| < +\infty$ (to ensure $X_n$ are uniformly integrable).
1. Suppose $Y \le X_n$. Then $\mathbb{E}[\liminf_{n} X_n] \le \liminf_{n} \mathbb{E}[X_n]$.
2. Suppose $X_n \le Y$. Then $\mathbb{E}[\limsup_{n} X_n] \ge \limsup_{n} \mathbb{E}[X_n]$.
