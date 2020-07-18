---
layout: post
title:  "Notes on Probability Theory"
date:   2019-10-21 01:30:00 -0500
author: Siberian Tiger
categories: math
---

# Table of contents

- [Table of contents](#table-of-contents)
  - [Prologue](#prologue)
  - [Probability as a measure](#probability-as-a-measure)
    - [Probability space](#probability-space)
    - [Sample space](#sample-space)
    - [Discrete probability space](#discrete-probability-space)
    - [$\sigma$-field](#math-xmlnshttpwwww3org1998mathmathmlsemanticsmrowmiσmimrowannotation-encodingapplicationx-texsigmaannotationsemanticsmathσ-field)
      - [Intersection of $\sigma$-fields](#intersection-of-math-xmlnshttpwwww3org1998mathmathmlsemanticsmrowmiσmimrowannotation-encodingapplicationx-texsigmaannotationsemanticsmathσ-fields)
      - [Borel $\sigma$-field](#borel-math-xmlnshttpwwww3org1998mathmathmlsemanticsmrowmiσmimrowannotation-encodingapplicationx-texsigmaannotationsemanticsmathσ-field)
    - [Measure and probability](#measure-and-probability)
    - [Continuity of probability measures](#continuity-of-probability-measures)
    - [Caratheodory's extension theorem and the extension to a probability space](#caratheodorys-extension-theorem-and-the-extension-to-a-probability-space)
      - [Uniform measure on $[0, 1]$](#uniform-measure-on-math-xmlnshttpwwww3org1998mathmathmlsemanticsmrowmo-stretchyfalsemomn0mnmo-separatortruemomn1mnmo-stretchyfalsemomrowannotation-encodingapplicationx-tex0-1annotationsemanticsmath01)
      - [Uniform measure on $\lbrace 0, 1\rbrace^{\infty}$](#uniform-measure-on-math-xmlnshttpwwww3org1998mathmathmlsemanticsmrowmo-stretchyfalsemomn0mnmo-separatortruemomn1mnmsupmo-stretchyfalsemomi-mathvariantnormalmimsupmrowannotation-encodingapplicationx-texlbrace-0-1rbraceinftyannotationsemanticsmath01)
    - [Conditional probability](#conditional-probability)
    - [Independence](#independence)
    - [Borel-Cantelli lemma](#borel-cantelli-lemma)
    - [Combinatorial probability](#combinatorial-probability)
      - [$e$ as a limit](#math-xmlnshttpwwww3org1998mathmathmlsemanticsmrowmiemimrowannotation-encodingapplicationx-texeannotationsemanticsmathe-as-a-limit)
      - [Stirling's formula](#stirlings-formula)
      - [Permutations](#permutations)
      - [Mafia game](#mafia-game)
      - [Ordered lists and unordered lists](#ordered-lists-and-unordered-lists)
      - [Birthday paradox](#birthday-paradox)
      - [Coupon collection problem](#coupon-collection-problem)
  - [Expectation as Lebesgue integration](#expectation-as-lebesgue-integration)
    - [Random variables](#random-variables)
      - [Measurable functions](#measurable-functions)
    - [Cumulative distribution functions](#cumulative-distribution-functions)
    - [Independence of random variables](#independence-of-random-variables)
    - [Lebesgue integral and expectation of a general random variable](#lebesgue-integral-and-expectation-of-a-general-random-variable)
    - [Monotone convergence theorem](#monotone-convergence-theorem)
      - [Application of MCT: Approximating $g$ from below using special simple functions](#application-of-mct-approximating-math-xmlnshttpwwww3org1998mathmathmlsemanticsmrowmigmimrowannotation-encodingapplicationx-texgannotationsemanticsmathg-from-below-using-special-simple-functions)
      - [Application of MCT: Proof of linearity of Lebesgue integral](#application-of-mct-proof-of-linearity-of-lebesgue-integral)
      - [Application of MCT: Proof of Boral-Cantelli lemma](#application-of-mct-proof-of-boral-cantelli-lemma)
    - [Fatou's lemma](#fatous-lemma)
    - [Dominated convergence theorem](#dominated-convergence-theorem)
      - [Bounded convergence theorem](#bounded-convergence-theorem)
    - [Product measures](#product-measures)
    - [Fubini's theorem](#fubinis-theorem)
      - [$\sigma$-finite measures](#math-xmlnshttpwwww3org1998mathmathmlsemanticsmrowmiσmimrowannotation-encodingapplicationx-texsigmaannotationsemanticsmathσ-finite-measures)
      - [Non-negativity](#non-negativity)
  - [Special random variables](#special-random-variables)
    - [Continuous random variables](#continuous-random-variables)
    - [Review of infinite integrals](#review-of-infinite-integrals)
    - [Discrete random variables](#discrete-random-variables)
    - [Expectation and its properties](#expectation-and-its-properties)
    - [Expectation and its properties](#expectation-and-its-properties-1)
      - [Properties of expectation](#properties-of-expectation)
      - [Comments on expectation](#comments-on-expectation)
      - [Expectation of some discrete distributions](#expectation-of-some-discrete-distributions)
    - [Covariance and correlation coefficient](#covariance-and-correlation-coefficient)
    - [Indicator random variables](#indicator-random-variables)
    - [Memoryless distributions](#memoryless-distributions)
    - [Gaussian distributions](#gaussian-distributions)
      - [Tails](#tails)
    - [Expectations of a continuous random variable](#expectations-of-a-continuous-random-variable)
      - [Properties of expectations](#properties-of-expectations)
    - [Joint density and jointly continuous random variables](#joint-density-and-jointly-continuous-random-variables)
    - [Conditional probability density functions](#conditional-probability-density-functions)
    - [Bivariate normal random variables](#bivariate-normal-random-variables)
    - [Conditional expectation](#conditional-expectation)
    - [Derived distributions](#derived-distributions)
    - [Bivariate normal in polar coordinates](#bivariate-normal-in-polar-coordinates)
    - [Sum of two independent random variables](#sum-of-two-independent-random-variables)
    - [Moment generating function](#moment-generating-function)
      - [Uniqueness of MGF](#uniqueness-of-mgf)
      - [Properties of MGF](#properties-of-mgf)
    - [Probability generating function](#probability-generating-function)
    - [Spectral properties of symmetric matrices](#spectral-properties-of-symmetric-matrices)
    - [Three definitions of multivariate normal distributions](#three-definitions-of-multivariate-normal-distributions)
    - [Equivalence of the three definitions of multivariate normal distributions](#equivalence-of-the-three-definitions-of-multivariate-normal-distributions)
    - [Characteristic functions](#characteristic-functions)
  - [Limit laws of random variables](#limit-laws-of-random-variables)
    - [Modes of convergence](#modes-of-convergence)
    - [Useful inequalities](#useful-inequalities)
    - [Law of large numbers](#law-of-large-numbers)
    - [Central limit theorem](#central-limit-theorem)
    - [The Chernoff bounds](#the-chernoff-bounds)
  - [Stochastic processes](#stochastic-processes)
    - [Random walks](#random-walks)
    - [Branching processes](#branching-processes)
    - [Poisson processes](#poisson-processes)
      - [Properties of Poisson processes](#properties-of-poisson-processes)
    - [Markov chains](#markov-chains)
      - [Steady state distribution / stationary distribution](#steady-state-distribution--stationary-distribution)
      - [Recurrence and transience](#recurrence-and-transience)
    - [Uniqueness of the stationary distribution](#uniqueness-of-the-stationary-distribution)
    - [Ergodicity](#ergodicity)
    - [Periodicity and mixing](#periodicity-and-mixing)
    - [Periodicity and mixing](#periodicity-and-mixing-1)
    - [PageRank algorithm](#pagerank-algorithm)
    - [Conditional expectation](#conditional-expectation-1)
    - [Martingale](#martingale)
    - [Martingale properties](#martingale-properties)
    - [Doob's decomposition](#doobs-decomposition)
    - [Stopping theorem](#stopping-theorem)
    - [Doob-Kolmogorov inequality](#doob-kolmogorov-inequality)

------

This post is based on a course that I took in fall, 2019. 
I refine it aperiodically for the purpose of summarizing and promoting my understanding.

> Updates  
> May 2, 2020: structured the notes.  
> July 9, 2020: rewrote the Chernoff bounds.

## Prologue

Although a real analysis background is not necessary, we expect the readers to be familar with the manipulations of limits such as $\limsup$ and $\liminf$.

The notes cover three topics:
- Measure Theory Foundations. Learning measure theory is like learning words before making sentences.
- Laws of Probability. Including Laws of Large Numbers and Central Limit Theorems.
- Stochastic Processes. Like Poisson processes, Markov chains and martingales.

## Probability as a measure

### Probability space

Probability is about quantifying uncertainty. To this end, a triple $(\Omega, \mathcal{F}, \mathbb{P})$ called probability space is needed, where $\Omega$ is a sample space, $\mathcal{F}$ is a $\sigma$-field, and $\mathbb{P}$ is a probability measure. Now we look at them in details.

### Sample space

A **sample space** $\Omega$ is an arbitrary set. It can be 
- finite, e.g. $\lbrace 1, 2, \cdots, n\rbrace$,
- countable, e.g. $\lbrace a_1, a_2, \cdots, a_n, \cdots\rbrace$, $\mathbb{Z}$ (integers), $\mathbb{Q}$ (rational numbers), or 
- uncountable, $\lbrace 0, 1\rbrace^{\infty}$ (set of all infinite sequences of zeros and ones). 

Elements of the sample space are called **elementary outcomes** and denoted by $\omega$.

Here are some examples of sample spaces.

1. Roll a die once. $\Omega = \lbrace 1, 2, 3, 4, 5, 6\rbrace$. The $\Omega$ here is finite.
2. Roll a die 10 times. $\Omega = \lbrace 1, 2, 3, 4, 5, 6\rbrace^{10} = \lbrace (a_1, \cdots, a_{10}): a_i \in \lbrace 1, \cdots, 6\rbrace, i = 1, \cdots, 10\rbrace$. In this case, $(3, 1, 1, 4, 5, 6, 5, 4, 3, 1)$ is an $\omega$. The $\Omega$ here is finite.
3. $\Omega = \mathbb{Z}_{+}$ (non-negative integers). The $\Omega$ here is countable.
4. $\Omega = \lbrace 0, 1\rbrace^{\infty}$. This is the sample space of tossing a coin for infinite times. The $\Omega$ here is uncountable.

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
   - $\Omega = \lbrace (0, 0), (0, 1), (1, 0), (1, 1)\rbrace$;
   - $\lvert\mathcal{F}\rvert = 2^4 = 16$;
   - $\mathbb{P}((0, 0)) = \mathbb{P}((0, 1)) = \mathbb{P}((1, 0)) = \mathbb{P}((1, 1)) = 1/4$.
2. $\Omega = \lbrace 3, \text{DAVID}, 15.085\rbrace$, each elementary outcome with probability $0.3$, $0.1$ and $0.6$.
3. Poisson discrete probability space. For a fixed $\lambda > 0$, take $\Omega = \mathbb{Z} _{+}$. Then $\mathbb{P}(n) = \frac{\lambda^n}{n!} e^{-\lambda}$. To verify the third condition of discrete probability space, notice that $\sum _{n=0}^{\infty} \mathbb{P}(n) = e^{-\lambda}\sum _{n=0}^{\infty}\frac{\lambda^n}{n!} = e^{-\lambda} \cdot e^{\lambda} = 1$.

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
1. $\emptyset \in \mathcal{F}$ (this ensures that $\mathcal{F}$ is non-empty);
2. if $A \in \mathcal{F}$, then $A^c \in \mathcal{F}$;
3. if $A_1, A_2, \cdots, A_n, \cdots \in \mathcal{F}$, then $\cup_{n=1}^{\infty} A_n \in \mathcal{F}$. 

By de Morgan's laws, the third condition also has implications for intersection.

We now give some examples of $\sigma$-fields.
1. Given $\Omega$, the simplest $\mathcal{F} = \lbrace \emptyset, \Omega\rbrace$.
2. Given $\Omega = \lbrace 1, \cdots, 6\rbrace^{\infty}$, let $A = \lbrace (w_1, w_2, \cdots): 1 \le w_1 \le 2\rbrace, B = \lbrace (w_1, w_2, \cdots): 3 \le w_1 \le 4\rbrace, C = \lbrace (w_1, w_2, \cdots): 5 \le w_1 \le 6\rbrace$. Then $\mathcal{F} = \lbrace \emptyset, A, B, C, A\cup B, B\cup C, A\cup C, A\cup B\cup C\rbrace$. This is our first nontrivial example of $\sigma$-fields. 
3. All subsets of $\Omega$.

#### Intersection of $\sigma$-fields

*Proposition.* Let $\lbrace \mathcal{F} _s\rbrace$ be a set of $\sigma$-fields. Then $\mathcal{F} = \bigcap _{s} \mathcal{F} _s = \lbrace A\subset \Omega: A \in \mathcal{F}_s, \forall s\rbrace$ is also a $\sigma$-field.

*Proof.*
1. $\emptyset \in \mathcal{F}_s, \forall s \Rightarrow \emptyset \in \mathcal{F}$.
2. Suppose $A \in \mathcal{F} \Rightarrow A \in \mathcal{F}_s, \forall s \Rightarrow A^c \in \mathcal{F}_s, \forall s \Rightarrow A^c \in \mathcal{F}$.
3. Exercise.

#### Borel $\sigma$-field

Take any set $\mathcal{C}$ of subsets of $\Omega$. Define $\sigma(\mathcal{C})$ as the intersection of all $\sigma$-fields containing $\mathcal{C}$.

*Example.* $\Omega = \lbrace 1, 2, 3, 4, 5, 6\rbrace$, $\mathcal{C} = \lbrace (1, 2), (3, 4), (5, 6)\rbrace$. Then $\sigma(\mathcal{C}) = \lbrace \emptyset, (1, 2), (3, 4), (5, 6), (1, 2, 3, 4), (3, 4, 5, 6), (1, 2, 5, 6), (1, 2, 3, 4, 5, 6)\rbrace$, similar to the second example of $\sigma$-fields.

Now take $\Omega = [0, 1]$. Let $\mathcal{C}$ be all closed intervals, i.e. $\mathcal{C} = \lbrace [a, b]: 0\le a\le b\le 1\rbrace$. Then $\sigma(\mathcal{C})$ is called **Borel $\sigma$-field**. Note that Borel $\sigma$-field does *not* contain all subsets of $[0, 1]$. 

### Measure and probability

Given $(\Omega, \mathcal{F})$, a **measure** is a function $\mu: \mathcal{F} \rightarrow \mathbb{R}_{+}$, such that
1. $\mu(\emptyset) = 0$;
2. if $\lbrace A_i, i = 1, 2, \cdots\rbrace$ is a countable sequence of *disjoint* elements of $\mathcal{F}$, then $\mu(\cup_{i=1}^{\infty} A_i) = \sum_{i=1}^{\infty}\mu(A_i)$ (sum of numbers). 'Disjoint' means $A_i \cap A_j = \emptyset, \forall i \neq j$.

Measures are a generalization of volumes. 

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

#### Uniform measure on $\lbrace 0, 1\rbrace^{\infty}$

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

*Definition.* $\lbrace A_n, i.o.\rbrace = \cap_{n=1}^{\infty} \cup_{i=n}^{\infty} A_i$. It means events that occurs infinitely often.

*Borel-Cantelli lemma.*  
1. Suppose $\lbrace A_n, n\ge 1\rbrace$ is a sequence of events such that $\sum_{i=1}^{\infty} \mathbb{P}(A_n) < +\infty$, then $\mathbb{P}(A_n, i.o.) = 0$.
2. Suppose $\lbrace A_n, n\ge 1\rbrace$ is a sequence of events such that $\sum_{i=1}^{\infty} \mathbb{P}(A_n) = +\infty$ and $A_n$ are independent, then $\mathbb{P}(A_n, i.o.) = 1$.

Proof of Borel-Cantelli lemma.

- Use union bounds.
- Use the following lemma. $0 \le p_n \le 1, \forall n \in \mathbb{N}$. Suppose $\sum_{n=1}^{\infty} p_n = +\infty$. Then $\prod_{i=1}^{\infty} (1-p_i) = 0$. The proof of this lemma uses the concavity of $\log(1-x)$.

### Combinatorial probability

#### $e$ as a limit

- $\lim_{n\rightarrow \infty} (1+\frac{1}{n})^n = e$.
- For any $a_n \rightarrow a$, $\frac{b_n}{n} \rightarrow 1$ as $n\rightarrow \infty$, $(1+\frac{a_n}{n})^{b_n} \rightarrow e^a$. (Proof by Taylor approximation)

#### Stirling's formula

$n! \approx \frac{n^{n+\frac{1}{2}}}{e^n}\sqrt{2\pi}$.

#### Permutations

$n!$.

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

- Suppose $c > 1$, then $\lim_{n\rightarrow \infty} \mathbb{P}(\lbrace c_1, \cdots, c_t\rbrace = \lbrace 1, \cdots, n\rbrace) = 1$.
- Suppose $c < 1$, then $\lim_{n\rightarrow \infty} \mathbb{P}(\lbrace c_1, \cdots, c_t\rbrace = \lbrace 1, \cdots, n\rbrace) = 0$.

*Proof* for the *Theorem* when $c > 1$.
- Let $A_t$ denote the event that not all coupon collected up to $t$. It remains to show $\mathbb{P}(A_t) \rightarrow 0$.
- $A_t = \cup_{i=1}^{n} B_{t, i}$, where $B_{t, i}$ denotes that coupon $i$ is not collected.
- Apply union bound, and show $\mathbb{P}(B_{t, i}) \rightarrow 0$ by Taylor approximation.

## Expectation as Lebesgue integration

### Random variables

*Definition.*
Given $(\Omega, \mathcal{F})$, $\forall c \in \mathbb{R}, X^{-1}(c) = \lbrace \omega \in \Omega: X(w) \le c\rbrace \in \mathcal{F}$.

Extended-valued r.v.: $\Omega \rightarrow \mathbb{R}\cup \lbrace +\infty\rbrace$.

Indicator function $I_A$.

Simple random variables.  
*Definition.* (Different from lecture notes) $X: \Omega \rightarrow \mathbb{R}$ is simple if $\lvert\text{Im}(X)\rvert < +\infty$, where $\text{Im}(X)$ is the set of all values realized by $X$. Here $\text{Im}$ denotes the image of a function (image is opposed to preimage).

If $X$ is simple, $X = \sum_{i=1}^m x_i I_{A_i}$.

#### Measurable functions

$(\mathcal{F}_1, \mathcal{F}_2)$-measurable , i.e. generalization of random variables. Given $(\Omega_1, \mathcal{F}_1)$, $(\Omega_2, \mathcal{F}_2)$. $X: \Omega_1 \rightarrow \Omega_2$ is called $(\mathcal{F}_1, \mathcal{F}_2)$-measurable if $\forall B \in \mathcal{F}_2$, $X^{-1}(B) = \lbrace \omega \in \Omega_1: X(\omega) \in B\rbrace \in \mathcal{F}_1$.

A r.v. is a special case with $(\Omega_2, \mathcal{F}_2) = (\mathbb{R}, \mathcal{B})$.

### Cumulative distribution functions

*Definition.* $F_X: \mathbb{R} \rightarrow [0, 1]$ defined by $F_X(x) = \mathbb{P}(X \le x)$.

*Theorem.* Given a r.v. $X$, $F_X$ satisfies
1. monotinicity;
2. $\lim_{x\rightarrow -\infty} F_X(x) = 0$, $\lim_{x\rightarrow +\infty} F_X(x) = 1$;
3. right-continuity, i.e. $\forall x\in \mathbb{R}$, $\lim_{y\downarrow x} F_X(y) = F_X(x)$.

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

*Proof (part 1.2).*  
Suppose $g = q = \sum_{i=1}^{m} a_i 1 _{A_i}$ is simple and $\int q d\mu < +\infty$.
Let $S = \lbrace i: a_i > 0\rbrace$, $A = \bigcup _{i \in S} A_i$, $B_n = \lbrace \omega\in A: g_n(\omega) \ge q(\omega) - 1/r\rbrace$, where $0 < 1/r < \min_i a_i$.

Then $\int g_n d\mu + \int 1/r 1 _{B_n} d\mu \ge \int q 1 _{B_n} d\mu$. Eventually, show that $\lim _{n\rightarrow \infty} \int g_n d\mu \ge \int q d\mu$.  
On the other hand, $\lim _{n\rightarrow \infty} \int g_n d\mu \le \int q d\mu$, which concludes the proof.

*Proof (part 2).*  
For a general $g$, recall $\int g d\mu = \sup_{q\in S(g)} \int q d\mu$. Let $h_n = \min\lbrace g_n, q\rbrace$. Then $h_n \uparrow q$ a.s. By MCT, 
$\int q d\mu = \lim_{n\rightarrow \infty} \int \min\lbrace g_n, q\rbrace d\mu \le \lim_{n\rightarrow \infty} \int g_n d\mu$.  
Therefore, 
$\lim_{n\rightarrow \infty} \int g_n d\mu \ge \sup_{q \in S(g)} \int q d\mu = \int g d\mu$.  
On the other hand, $\lim_{n\rightarrow \infty} \int g_n d\mu \le \int q d\mu$, which concludes the proof.

Note that in general, $X_n \rightarrow X$ a.s. cannot give $\mathbb{E}X_n \rightarrow \mathbb{E}X$.

*Example.* $U$ uniform at random from $[0, 1]$.
Let $X(u) = n$ if $u \in [0, 1/n]$ and $X(u) = 0$ otherwise. 
$X_n \rightarrow 0$ a.s. 
However, $\mathbb{E}X_n \not\rightarrow \mathbb{E}0 = 0$.

#### Application of MCT: Approximating $g$ from below using special simple functions

For $r \in \mathbb{N}$, define $g_r(w) = i/(2^r)$ if $g(w) < r$ and $g(w) \in [i \in 2^r, (i + 1) / 2^r]$, and $g_r(w) = r$ if $g(w) \ge r$.

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

*Proof.*
1. Fix $n \ge 1$, $\inf_{k \ge n} (X_k - Y) \le X_m - Y$ for all $m \ge n$. Taking expectation, $\mathbb{E}[\inf_{k \ge n} (X_k - Y)] \le \inf_{m\ge  n}\mathbb{E}[X_m - Y]$. Taking limit as $n \rightarrow \infty$, and apply MCT on the left side.
2. Similar to 1.

Let $Y = 0$. Fatou's lemma states that if $X\ge 0$, a.s., then $\mathbb{E}[\liminf_{n} X_n] \le \liminf_{n} \mathbb{E}[X_n]$.

### Dominated convergence theorem

*Theorem.* 
Suppose $(X_n, n\ge 1)$, $X_n \rightarrow X$ a.s., and $\exists Y$, such that $\lvert X_n \rvert \le Y$, and $\mathbb{E}[Y] < +\infty$. Then $\mathbb{E}[\lim_{n\rightarrow \infty} X_n] = \lim_{n\rightarrow \infty} X_n$.

*Proof.*
Note that $-Y \le X_n \le Y$. Apply Fatou's lemma.

#### Bounded convergence theorem

($Y$ is constant in DCT.) Suppose $\lvert X_n \rvert \le C$, a.s..

### Product measures

Motivation: $(X_n, n \ge 1)$ i.i.d.. In what probability space does the sequence exist?

Given $(\Omega_1, \mathcal{F}_1, \mathbb{P}_1)$ and $(\Omega_2, \mathcal{F}_2, \mathbb{P}_2)$, define their product measure as $(\Omega_1 \times \Omega_2, \mathcal{F}_1 \times \mathcal{F}_2, \mathbb{P}_1 \times \mathbb{P}_2)$, where
- $\Omega_1 \times \Omega_2$ = Cartesian product
- $\mathcal{F}_1 \times \mathcal{F}_2$ = smallest $\sigma$-field containing all sets $A_1\times A_2$ where $A_1\in \mathcal{F}_1$, $A_2\in \mathcal{F}_2$.
- $\mathbb{P}_1 \times \mathbb{P}_2(A_1\times A_2) = \mathbb{P}_1(A_1) \cdot \mathbb{P}_2(A_2)$. Then extended by Caratheodory's extension theorem.

Goal: Given $F: \mathbb{R} \mapsto [0, 1]$ CDF, construct $X_1, X_2$ such that $X_1\perp X_2$ and $F_{X_1} = F_{X_2} = F$.  
- $X_1: \Omega \times \Omega \rightarrow \mathbb{R}$, $X_1(\omega_1, \omega_2) = X(\omega_1)$.
- $X_2: \Omega \times \Omega \rightarrow \mathbb{R}$, $X_2(\omega_1, \omega_2) = X(\omega_2)$.

Then $\mathbb{P}(X_1\le t_1, X_2\le t_2) = F_X(t_1) F_X(t_2)$.

### Fubini's theorem

Let $Y(\omega_1) = \int X(\omega_1, \omega_2) d\mathbb{P}_2$. Let $Z(\omega_2) = \int X(\omega_1, \omega_2) d\mathbb{P}_1$. The question is, whether $\int Y d\mathbb{P}_1 = \int Z d\mathbb{P}_2 = \int X d\mathbb{P}_1\times \mathbb{P}_2$. 

Fubini's theorem provides a sufficient condition.

*Theorem [Fubini 1].*
Suppose $X\ge 0$, a.s.. Then
1. For almost every $\omega_1 \in \Omega_1$, $X(\omega_1, \omega_2): \Omega_2 \mapsto \mathbb{R}$ is measurable.
2. For almost every $\omega_2 \in \Omega_2$, $X(\omega_1, \omega_2): \Omega_1 \mapsto \mathbb{R}$ is measurable.
3. $\int X(\omega_1, \omega_2) d\mathbb{P}_2$ is a measurable function of $\omega_1$.
4. $\int X(\omega_1, \omega_2) d\mathbb{P}_1$ is a measurable function of $\omega_2$.
5. $\int _{\Omega_1} [\int _{\Omega_2} X(\omega_1, \omega_2) d\mathbb{P}_2] d\mathbb{P}_1 = \int _{\Omega_2} [\int _{\Omega_1} X(\omega_1, \omega_2) d\mathbb{P}_1] d\mathbb{P}_2 = \int _{\Omega\times \Omega_2} X(\omega_1, \omega_2) d\mathbb{P}_1 \times \mathbb{P}_2$.

*Theorem [Fubini 2].*
Suppose $\int \lvert X(\omega_1, \omega_2) \rvert d\mathbb{P}_1 \times \mathbb{P}_2 = \mathbb{E}[\lvert X \rvert] < +\infty$, then 1-5 hold.

#### $\sigma$-finite measures

In general, Fubini's theorem holds for $\sigma$-finite measures.

*Definition.*
$(\Omega, \mathcal{F}, \mu)$ is $\sigma$-finite if $\exists A_n \in \mathcal{F}$, such that $A_n \subset A_{n+1}, \forall n$, and that $\bigcup_n A_n = \Omega$, $\mu(A_n) < +\infty$.

Counting measure on $\mathbb{R}$: $\mu(A) = \lvert A\rvert$ when $\lvert A\rvert < +\infty$, and $\mu(A) = \infty$ otherwise. $\mathbb{R} \neq \bigcup_n A_n$ where $\lvert A\rvert < +\infty$. In this case, you cannot change the order of the integrals.

#### Non-negativity

*Counter-example.*

## Special random variables

### Continuous random variables

*Definition.* A random variable $X$ is continuous if $\exists f: \mathbb{R}\mapsto \mathbb{R} _{+}$, such that $F_X(x) = \int _{-\infty}^{x} f(t) dt$ (Riemann integral).
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

### Expectation and its properties

Discrete r.v. $X$. 

*Fact.* 
$\mathbb{E}[X] = \sum_{n\ge 0}[X\ge n] = \sum_{n\ge 1}[X\ge n]$.

*Theorem.* 
$\mathbb{E}[g(X)] = \sum_{x: p_X(x) \ge 0} g(X) p_{X}(x)$.

*Definitions.*
1. $\mathbb{E}[X^k]$: $k$th moment.
2. $\mathbb{E}[(X - \mathbb{E}[X])^k]$: $k$th central moment.
3. Variance is second central moment.
4. Standard deviation is $\sqrt{\operatorname{VAR}(X)}$.

$X \ge 0$ a.s. $\iff$ $\mathbb{P}(\lbrace \omega: X(\omega)\ge 0\rbrace) = 1$.

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

This first property is proved by the Cauchy-Schwarz inequality $(\mathbb{E}[XY])^2 \le \mathbb{E}[X^2]\cdot \mathbb{E}[Y^2]$.  
Proof using $\mathbb{E}[(X-tY)^2] \ge 0$.

### Indicator random variables

*Definition.*
$I_A: \Omega \mapsto \lbrace 0, 1\rbrace$.

- $I_{A^c} = 1 - I_A$.
- $I_{A\cap B} = I_A \cdot I_B$.

Indicator r.v. can be used to prove $\mathbb{P}(A\cup B) = \mathbb{P}[A] + \mathbb{P}[B] - \mathbb{P}[A\cap B]$.

### Memoryless distributions

Review: Continuous random variables

*Definition.*

*Comment.*  
- If $f$ is a PDF, $E = \lbrace t: f(t) < 0\rbrace$, $\mu(E) = 0$ (Lebesgue measure).
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
Suppose $X\ge 0$ is a continuous random variable, i.e. $\mathbb{P}(X\ge 0) = 1$, i.e. $\lbrace \omega: X(\omega)\ge 0\rbrace$ a.s. Let $f_X$ be its PDF. Then $\mathbb{E}[X] = \int_{0}^{\infty} \mathbb{P}(X > t) dt$.

$\mathbb{E}[g(X) = \int_{-\infty}^{+\infty} g(t) f_X(t) dt$.

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

Therefore, $f_{R, \Theta}(r, \theta) = f_R(r) f_{\Theta}(\theta)$, which means $R \perp \Theta$. $\Theta$ obeys the uniform distribution on $[0, 2\pi]$. Let $Z = R^2$. Then $f_Z(z) = 1/2 \exp(-z/2) \stackrel{d}{=} \operatorname{Exp}(1/2)$.

The PDF in polar coordinates can be used to show that the constant of a standard normal distribution is $C = 1/\sqrt{2\pi}$.

### Sum of two independent random variables

*Convolution formula.*
Given continuous r.v. $X, Y$, with $f_X$, $f_Y$, $X\perp Y$. Then $X + Y$ is a continuous random variable and 
$$
f_{X + Y}(z) = \int_{-\infty}^{+\infty} f_X(z) f_Y(z - t) dt.
$$

*Proof.*
1. Consider $g: (x, y) \mapsto (x + y, y)$, and use derived distribution.
2. Take marginal density.

### Moment generating function

$M_X(s) = \mathbb{E}[e^{sX}]$.

*Example.* (Exponential distributions)
$D_X = (-\infty, \lambda)$.

*Example.* (Normal distributions)
$D_X = (-\infty, +\infty)$.

*Example.* (Power distributions)
$D_X = (-\infty, 0]$.

Domain $D_X$ of MGF: 
- always an interval;
- always contains $0$.

*Fact.*
Suppose $M_X(s) < +\infty$ for some $s > 0$. Then $\forall s'\in (0, s)$, $M_X(s') < +\infty$.
Suppose $M_X(s) < +\infty$ for some $s < 0$. Then $\forall s'\in (s, 0)$, $M_X(s') < +\infty$.

Suppose $\limsup_{x\rightarrow \infty} \frac{\log \mathbb{P}(X > x)}{x} = -\gamma < 0$, then $D_X \supset [0, \gamma)$.

If $D_X \supset (-\delta, \delta)$, then the tails of $X$ decay exponentially fast.

#### Uniqueness of MGF

*Theorem.*
Suppose $M_X(s)$ is finite, $\forall s \in [-a, a]$ for some $a > 0$. Then $M_X$ uniquely determines the distribution of $X$.

#### Properties of MGF

- $X\perp Y$. $M_{X+Y}$
- $Y = aX + b$.
- $X\perp Y$. $M_{aX + bY}$.

Moment generating property.

### Probability generating function

$X = 0, 1, 2, \cdots \in \mathbb{Z}_{+}$.
$g(s) = \sum_{n=0}^{\infty} s^n p_n$.

Probability generating property: 
$$\frac{1}{m} \frac{d^m g(0)}{d s^m} = p_m.$$

$\mathbb{E}X = \dot{g}(1)$.

$D_X \supset [0, 1]$ trivially.

Note: $g(s) = M_X(\log s)$.

### Spectral properties of symmetric matrices

### Three definitions of multivariate normal distributions

*Definition 1 (of non-degenerate m.v.n.).*

*Definition 2.*
$X = DW + \mu$.

*Definition 3.*


### Equivalence of the three definitions of multivariate normal distributions


### Characteristic functions

*Definition.*

*Inversion theorem.*

## Limit laws of random variables

### Modes of convergence

1. Almost surely convergence.
   
2. Convergence in distribution.
   
3. Convergence in probability.

4. Convergence in terms of characteristic functions.

Hierarchy of the modes of convergence

### Useful inequalities

*Markov's inequality.*

*Chebyshev's inequality.*
$\mathbb{P}(|X - \mathbb{E}[X]| \ge \epsilon) \le \frac{\sigma^2}{\epsilon^2}$.

### Law of large numbers

*Theorem.* (Strong LLN)
$S_n / n \xrightarrow{a.s.} \mathbb{E}[X_1]$.

*Theorem.* (Weak LLN)
$S_n / n \xrightarrow{i.p.} \mathbb{E}[X_1]$.

The proof the WLLN is much easier than that of the SLLN.
One method is by Chebyshev's inequality assuming bounded variance; another method is by characteristic functions.

### Central limit theorem

*Lindeberg-Lévy CLT.*
$$
\frac{S_n - n\mu}{\sigma \sqrt{n}} \xrightarrow{d} N(0, 1).
$$

The proof the Lindeberg-Lévy CLT relies on Taylor expansion.
The Lindeberg-Lévy CLT implies the WLLN, but not the SLLN.

*Berry-Esseen CLT.*

*Local CLT.*
$X_i \in \mathbb{Z}$.
$\mathbb{P}(S_n = m)$

### The Chernoff bounds

For random variables $X_1, \cdots, X_n$ and $S_n = \sum_{i=1}^{n} X_i$, the general Chernoff bounds comprises an upper bound and a lower bound on $\mathbb{P}(S_n \ge t)$. By default, the Chernoff bound refers to the upper bound. Below we let $\mu := \mathbb{E}[S_n]$.

*Upper bound*.
Assume $X_i$ are i.i.d.. For any $t > \mu$, let $\phi(a) = \sup_{s\ge 0} \{ as - \log M(s) \}$, where $M(s)$ is the MGF of $X_i$. Then $\mathbb{P}(S_n > t) \le \exp( -n \phi(t/n) )$.

Applying Markov's inequality to the MGF of $S_n$ completes the proof.
It is direct to extend the bound to the non-i.i.d. case.
For non-i.i.d. Bernoulli random variables, with different relaxations, there are an additive form and a multiplicative form of the Chernoff bound.

*Additive form (Lecture notes of THU ML).*
For any $t > \mu$, we have $\mathbb{P}(S_n > t) \le \exp( -n D_{B}^{e}(t/n || \mu/n) )$ if $t\le n$, where $D_{B}^{e}(p || q) := p \log (p / q) + (1 - p) \log ((1 - p) / (1 - q))$.

Obviously, if $t > n$ then $\mathbb{P}(S_n > t) = 0$. 
Notice that $D_{B}^{e}(t/n || \mu/n) \ge 2(t - \mu)^2 / n^2$.
Collectively, $\mathbb{P}(S_n > t) \le \exp( - 2(t - \mu)^2 / n )$ holds for all $t\ge \mu$, which is precisely Hoeffding's inequality applied to Bernoulli random variables.

*Multiplicative form (High-Dimensional Probability).*
For any $t > \mu$, we have $\mathbb{P}(S_n > t) \le \exp(-\mu) (e\mu / t)^t$.

The multiplicative form implies that $\mathbb{P}(S_n - \mu > \delta \mu) \le \exp(-\mu \delta^2 / 3)$ if $\delta \in (0, 1]$, and $\mathbb{P}(S_n - \mu > \delta \mu) \le \exp(-\mu \delta^2 / (2 + \delta))$ if $\delta > 1$.
Here $\delta$ can be interpreted as the relative error.

For $t \in [\mu, 2\mu)$ ($\delta \in (0, 1]$), the above bound can be transformed into $\mathbb{P}(S_n > t) \le \exp(- (t-\mu)^2 / (3\mu))$, which is tighter than Hoeffding's inequality.
Otherwise for $t > 2\mu$, Hoeffding's inequality is usually tighter. To see why, compare $\mathbb{P}(S_n > t) \le \exp(-(t - \mu))$ and $\mathbb{P}(S_n > t) \le \exp(-2(t-\mu)^2 / n))$ as $t - \mu$ grows linearly in $n$.

The bound in the multiplicative form is known as the Poisson tail (tail of the Poisson distribution). Under the condition of the Poisson limit theorem, intuitively the multiplicative bound should be sharp. Indeed, in this case, $t - \mu$ grows sublinearly in $n$. Then even for $t > 2\mu$, the mulplicative Chernoff bound is tighter than Hoeffding's inequality.

*Lower bound.*
$n^{-1} \log \mathbb{P}(S_n \ge t) \xrightarrow{n\rightarrow\infty} - \phi(t/n)$.

*Proof.*
**Change of measure.** 
Let $f_Y(x) = e^{s^{\star} x} f_X(x) / M(s^{\star})$.

## Stochastic processes

$X(\omega, \cdot)$: 

### Random walks

*Question.* 
What is $\mathbb{P}(\text{RW returns to zero})$?

### Branching processes

*Definition.*
$F$. Let PGF of $F$ be $g$.

*Question.*
Does the process continue indefinitely or die out?

*Theorem.*
Let $G_n$ be the PGF of $Z_n$, the number of offspring in generation $n$. 
Then $G_n = g^{(n)}$, i.e., apply $g$ for $n$ times.

*Theorem.* (Variance of $Z_n$)

*Theorem.* (Extinction probability $\eta$)

### Poisson processes

*Intuition.*
Bernoulli process.

*Definition.*

Does a Poisson process exist? 
An example by construction: generating a Poisson process with exponential distributions $T_n, n\ge 1$. 
$Y_n = \sum_{k=1}^{n} T_k$ mark the events of the counting process. $N(t) = \max\{n: S_n\le t\}$.

*Claim.* 
$N(t)$ is a Poisson process.

#### Properties of Poisson processes

*Claim.* 
$N(t) \stackrel{d}{=} \operatorname{Pois}(\lambda t)$.

*Claim.* 
$T_k = Y_k - Y_{k - 1}$. Then $T_k, k\ge 1$ are i.i.d. $\operatorname{Exp}(\lambda)$.

### Markov chains

*Definition.*

*Definition.* (Homogeneous Markov chains)

$P = (p_{ij}, 1\le i, j \le N)$.

*Notations.*  
$\nu^{\top}$, $\nu^{\top} P$.

#### Steady state distribution / stationary distribution

*Definition.* (Steady state / stationary distribution)

*Theorem.* (Existence of steady state distributions)

*Proof.*
Though the lens of linear programming.

#### Recurrence and transience

*Definition.* ($i \rightarrow j$, $i$ communicates with $j$)

*Definition.* (Recurrent and transient)

Let $R$ be all recurrent states. Let $T$ be all transient states.

*Lemma.* 
On $R$, the relation $\leftrightarrow$ is equivalency.

*Corollary.*
$N = T\cup R_1 \cup \cdots \cup R_r$.

Recurrence time $T_i$.

### Uniqueness of the stationary distribution

For a MC with a single recurrent class, i.e., $[N] = T \cup R$, we have the following lemmas.

1. For $i\in R$, $\mathbb{P}(X_n = i, i.o.) = 1$. 
2. Furthermore, let $T_i = \min_{n\ge 1} \{X_n = i \mid X_0 = i\}$. Then $\exists c > 0$, $0 < q < 1$, such that $\mathbb{P}(T_i \ge t) \le c q^t$, i.e., the tail probability decreases geometrically.

*Theorem.* (Uniqueness of the stationary distribution)  
MC with a single recurrent class has a unique stationary distribution $\pi$. 
For $i\in T$, $\pi_i = 0$.
For $i\in R$, $\pi_i = 1/\mathbb{E}[T_i] > 0$.

*Proof.*
The proof is long, and we leave that for your own studying.

### Ergodicity

Let $N_i = \sum_{n=0}^t 1_{X_n = i}$.

*Theorem.* (Ergodicity of MC)  
Assume a MC with a single recurrence class. For every state $k$ and every state $i$, when $X_0 = k$,
1. $\lim_{t\rightarrow \infty} N_i(t) / t = \pi_i$, a.s., (convergence of a r.v.)
2. $\lim_{t\rightarrow \infty} \mathbb{E}[N_i(t)] / t = \pi_i$. (convergence of a r.v.)

*Proof.*

### Periodicity and mixing

*Definition.* (period)  
Given state $x$, let $d_x$ period be the greatest common divisor of the set $I_x = \{n: p_{xx}^{(n)}\}$.

*Lemma.*
For all $x, y$ in the same recurrent class, $d_x = d_y$.

*Definition.*
A MC is called aperiodic if $d_x = 1$.

*Theorem.* (Mixing)  
Given an aperiodic MC $X_n$ with a single recurrence class, $\forall x, y$,
$\lim_{n\rightarrow \infty} p_{xy}^{(n)} = \lim_{n\rightarrow \infty} \mathbb{P}(X_n = y\mid X_0 = x) = \pi_y$.

Intuitively, the mixing theorem means "memoryless".

*Proof.* (Algebraic)  
An algebraic proof relies on Perron-Fronenius theorem. Here we only note that it shows
$|p_{xy}^{(n)} = \pi_y| \lesssim \lambda_2^n$, where $\lambda_2$ is the second largest e-value of $P$ and $|\lambda_2| < 1$.

Now we give an alternative proof with the coupling technique.

*Proof.* (Coupling)

### Periodicity and mixing

*Proof.* (Coupling)

### PageRank algorithm

Random surfer:
$\alpha \in (0, 1)$, transit according to $P$ with probability $1 - \alpha$ and jump to uniformly random state with probability $\alpha$.

Model webpage ranking by a MC. 
The ranking is given by the stationary distribution.

In surfing MC, $|p_{xy}^{(n)} - \pi_y| \le (1 - \alpha / N)^n$. 
Google uses $\alpha \approx 0.28$.
Here we compute $p_{xy}^{(n)}$ to approximate $\pi_y$.

### Conditional expectation

The most general form is $\mathbb{E}[X\mid \mathcal{G}]$ ($X$ is not necessarily measurable w.r.t. $\mathcal{G}$).

*Definition.* (Conditional expectation)
$\mathbb{E}[X\mid \mathcal{G}]$ is a random variable $Y\in \mathcal{G}$ and satisfies $\forall A \in \mathcal{G}$, 
$\mathbb{E}[Y 1_{A}] = \mathbb{E}[X 1_{A}]$.

*Tower property.*
$\mathcal{G}_1 \subset \mathcal{G}_2 \subset \mathcal{F}$.

### Martingale

*Definition.* (Filtration)

*Definition.* (Adaptation)  
$X_n$ adapted to $\{\mathcal{G}_n\}$.

*Definition.* (Martingale)

### Martingale properties

Sub-MG

Super-MG

*Theorem.*  
Let $\phi(\cdot)$ be a convex function. 

### Doob's decomposition

*Definition.* (Predictability)

*Theorem.* (Doob's decomposition)

**Martingale transform**

### Stopping theorem

*Definition.* Stopping time

Stopping time calculus

*Theorem.*

*Theorem.*

### Doob-Kolmogorov inequality

*Theorem.* (Doob-Kolmogorov inequality)  
Let $X_n\ge 0$ be a sub-MG sequence, $\epsilon > 0$ be arbitrary.
Then 
$$
\mathbb{P}(\max_{1\le m\le n} X_m > \epsilon) \le \frac{1}{\epsilon^2} \mathbb{E}[X_n^2].
$$

