---
layout: post
title:  "Notes on Inference and Information"
date:   2020-07-22 21:30:00 -0500
author: Siberian Tiger
categories: math
---

**Table of contents**

- [Notations](#notations)
- [Inequalities](#inequalities)
- [Exponential families](#exponential-families)
- [Typicality](#typicality)
- [Hypothesis testing](#hypothesis-testing)
- [Estimation](#estimation)
  - [Bayesian estimation](#bayesian-estimation)
  - [Non-Beysian estimation](#non-beysian-estimation)
- [Information measures](#information-measures)
  - [Discrete alphabets](#discrete-alphabets)
  - [Continuous alphabets](#continuous-alphabets)
- [Information geometry](#information-geometry)
- [Non-Bayesian modeling](#non-bayesian-modeling)
  - [Modeling via mixtures](#modeling-via-mixtures)
  - [Maximally ignorant priors](#maximally-ignorant-priors)
  - [Conjugate prior families](#conjugate-prior-families)
  - [Asymptotics of non-Bayesian modeling](#asymptotics-of-non-bayesian-modeling)
- [Approximation](#approximation)
  - [Stochastic approximation](#stochastic-approximation)
  - [Deterministic approximation](#deterministic-approximation)


------

This post is based on a course that I took in spring, 2020. 
I refine it aperiodically for the purpose of summarizing and promoting my understanding.

> Updates  
> July 22, 2020: added Beta distributions.

## Notations 

| | |
|-|-|
| upper-case letters $X, Y$ | random variables |
| lower-case letters $x, y$ | real numbers |
| $\mathcal{X}, \mathcal{Y}$ | alphabets |
| lower-case letters $p, q$ | PDFs or PMFs |
| | |

------

## Inequalities

- Jensen's inequality: for convex $f$, $\mathbb{E}[f(x)] \ge f(\mathbb{E}[x])$
- Log-sum inequality: $\sum_i a_i \log (a_i / b_i) \ge \sum_{i} a_i \log (\sum_{i} a_i / \sum_{i} b_i)$
  - Proof: Jensen's inequality, either by the convexity of $x\log x$ or the convexity of $-\log x$
- Gibbs' inequality: $\mathbb{E}_{p} [\log p] \ge \mathbb{E}_{p}[\log q]$

------

## Exponential families

- One-parameter exponential family (EF): $p_{Y}(y; x) = \exp\{ \lambda(x) t(y) - \alpha(x) + \beta(y) \}$
- $\lambda(x)$: natural parameter, $t(y)$: natural statistic, $\alpha(x)$: log partition function, $\beta(x)$: log base function
- Regular EF: the support of $P_{Y}(\cdot; x)$ does not depend on $x$
- Canonical EF: $\lambda(x) = x$, called linear in MIT 6.437
  - Geometric mean of two distributions
  - $q(y) = p_{Y}(y; 0)$: base function
- Natural EF: $\lambda(x) = x, t(y)=y$, called canonical in MIT 6.437
  - Tilting a distribution
- Properties of 1D canonical EF
  - $\dot{\alpha}(x) = \eta(x) := \mathbb{E}_{p_{Y}(\cdot; x)}[t(Y)]$: mean parameter
  - $\ddot{\alpha}(x) = \dot{\eta}(x) = J_{Y}(x)$: Fisher information
  - $D(p_{Y}(\cdot; x) || q(\cdot)) + \alpha(x) = x\eta(x)$
  - $d D(p_{Y}(\cdot; x) || q(\cdot)) / d\eta = x$
  - $d^2 D(p_{Y}(\cdot; x) || q(\cdot)) / d\eta^2 = 1/J_{Y}(x)$

------

## Typicality

- Normalized log-likelihood $L_{p}(y_{1}^{N}) = 1/N \sum_{n=1}^{N} \log p(y_n)$
- Typical set $\mathcal{T}_{\epsilon}(p; N)$: the set of sequences $y_{1}^{N}$ such that $|L_{p}(y_1^{N}) + H(p)| \le \epsilon$
- $P\{\mathcal{A}\} := \sum_{y_{1}^{N} \in \mathcal{A}} p^{N}(y_1^{N})$
- Asymptotic equipartition property (AEP)
  - AEP-1: $\lim_{N\to \infty} P\{\mathcal{T}_{\epsilon}(p; N)\} = 1$
  - AEP-2: for all $y_1^N \in \mathcal{T}_{\epsilon}(p; N)$, $2^{-N(H(p) + \epsilon)} \le p^{N}(y_1^N) \le 2^{-N(H(p) - \epsilon)}$
  - AEP-3: for sufficiently large $N$, $(1 - \epsilon) 2^{N(H(p) - \epsilon)} \le |\mathcal{T}_{\epsilon}(p; N)| \le 2^{N(H(p) + \epsilon)}$
- AEP for continuous distributions: $H(p) \to h(p)$, cardinality $|\cdot| \to \mathrm{vol}[\cdot]$ volume
- Normalized log-likelihood ratio $L_{p|q}(y_1^N) = 1/N \sum_{n=1}^{N} \log (p(y_n) / q(y_n))$
- Divergence typical set $\mathcal{T}_{\epsilon}(p|q; N)$: the set of sequences $y_{1}^{N}$ such that $|L_{p|q}(y_1^{N}) - D(p || q)| \le \epsilon$
- Equivalent in the sense that $\lim_{N\to \infty} P\{\mathcal{T}_{\epsilon}(p; N) \cap \mathcal{T}_{\epsilon}(p|q; N)\} = 1$
- For sufficiently large $N$, $(1 - \epsilon) 2^{-N(D(p || q) + \epsilon)} \le Q\{\mathcal{T}_{\epsilon}(p|q; N)\} \le 2^{-N(D(p || q) - \epsilon)}$
- Cramer's theorem: large deviation probability of sample averages
  - $Y_1^N$ i.i.d. from $q$ with finite mean $\mu < \gamma$
  - Chernoff exponent $E_C(\gamma) := D(p(\cdot; x) || q)$, where $p(y; x) = q(y) \exp\{xy - \alpha(x)\}$ such that $\mathbb{E}_{p(\cdot; x)}[y] = \gamma$
  - $\lim_{N\to \infty} -1/N \log \mathbb{P}(1/N \sum_{n=1}^N Y_n \ge \gamma) = E_C(\gamma)$
- Extensions to Cramer's theorem
  - Averages of functions of i.i.d. samples
  - Vector version
  - Beyond i.i.d. to samples from an ergodic random process: Gartner-Ellis theorem
- $\mathcal{P}_{N}^{\mathcal{Y}}$: the set of all types for sequences of length $N$ generated from an alphabet $\mathcal{Y}$
- Type class $\mathcal{T}_{N}^{\mathcal{Y}}(p)$: the set of sequences $y_1^N$ such that $\hat{p}(\cdot; y_1^N) = p(\cdot)$
- Properties of types
  - Polynomial number of types: $|\mathcal{P}_{N}^{\mathcal{Y}}| \le (N + 1)^{|\mathcal{Y}|}$
  - Probability of sequence as a function of its type: $q^N(y_1^N) = 2^{-N(D(\hat{p}(\cdot; y_1^N) || q) + H(\hat{p}(\cdot; y_1^N)))}$
  - Exponentially many sequences in each nondegenerate type class: $cN^{-|\mathcal{Y}|} 2^{NH(p)} \le |\mathcal{T}_{N}^{\mathcal{Y}}(p)| \le 2^{NH(p)}$, where $c$ depends on $p$ and $\mathcal{Y}$
  - Probability that a sequence in type $p$ is generated by $q$: $cN^{-|\mathcal{Y}|} 2^{-ND(p || q)} \le Q\{\mathcal{T}_{N}^{\mathcal{Y}}(p)\} \le 2^{-ND(p || q)}$
- Sanov's theorem: large deviation probability specified by $\mathcal{S}$
  - For $\mathcal{S} \subset \mathcal{P}^{\mathcal{Y}}$ and $q \in \mathcal{P}^{\mathcal{Y}}$, Chernoff exponent $D_{*}: = \inf_{p\in \mathcal{S}} D(p || q)$
  - $Q\{ \mathcal{S} \cap \mathcal{P}_{N}^{\mathcal{Y}} \} \le (N + 1)^{|\mathcal{Y}|} 2^{-ND_{*}}$
  - For $\mathcal{S}$ closed, the dominant atypical event converges in probability to the I-projection $p_{*} = \argmin_{p\in \mathcal{S}} D(p || q)$
  - More powerful than the scalar version of Cramer's theorem, but less powerful than its vector version
- Strongly typical set $\mathcal{T}_{\epsilon}^{\mathrm{S}}(p; N)$: the set of sequences $y_1^N$ such that $||\hat{p}(\cdot; y_1^N) - p(\cdot)||_{\infty} \le \epsilon$
  - Called "strong" not because of SLLN, but because it implies weaker typicality
  - Implies divergence typicality
  - Implies typicality, because for finite alphabets, typicality is an instance of divergence typicality where $q$ is the uniform distribution

------

## Hypothesis testing

- Bayesian hypothesis testing: likelihood ratio test (LRT)
- Neyman-Pearson hypothesis testing: no prior & no cost
- Randomized test
- Operatering characteristic (OC)
  - Efficient frontiers
  - Achievable operating points
- Minimax hypothesis testing: unknown prior $p$
  - In general $\min \max \ge \max \min$
  - $\min_{f} \max_{p\in [0, 1]} \phi(f, p) = \max_{p\in [0, 1]} \min_{f} \phi(f, p)$
- Asymptotics: 

------

## Estimation

### Bayesian estimation

- Sufficient statistics: 
- Bernstein-von Mises theorem: asymptotics of Bayesian estimation

### Non-Beysian estimation

- Valid: does not depend on $x$
- Admissible: valid and unbiased
- Minimum-variance unbiased (MVU) estimator
- Score function $S(y; x) = \partial \log p_{Y}(y; x) / \partial x$
- Fisher information $J_{Y}(x) = \mathbb{E}[S^2(y; x)] = - \mathbb{E}[\partial^2 \log p_{Y}(y; x) / \partial x^2]$
- Cramer-Rao (CR) bound: for all admissible $\hat{x}(\cdot)$, $\lambda_{\hat{x}}(x) \ge 1/J_{Y}(x)$
- Efficient estimator: satisfies CR bound with equality
  - Exists iff exponential family
  - Exists iff $\hat{x}(y) = x + S(y; x) / J_{Y}(x)$ is valid
  - Admissible, MVU, ML estimator
- Sufficient statistics: 
- Wald's theorem
- Cramer's theorem

------

## Information measures

### Discrete alphabets

- Bayesian modeling
- Entropy $H(p) = -\sum_{a} p(a) \log p(a)$
  - Nonnegative, by definition
  - Strictly concave, due to log-sum inequality
- Mutual information $I(X; Y) = I(Y; X) = H(X) - H(X | Y) = H(Y) - H(Y | X)$
  - Nonnegative, due to the nonnegativity of information divergence
  - $I(X; Y) = D(p_{X, Y} || p_{X} p_{Y}) = \sum_{x, y} p_{X, Y}(x, y) \log \frac{p_{X, Y}(x, y)}{p_{X}(x) p_{Y}(y)}$
  - $I(X; Y) = \sum_{X} p_{X}(x) D(p_{Y|X}(y|x) || p_{Y}(y)) = \sum_{Y} p_{Y}(y) D(p_{X|Y}(x|y) || p_{X}(x))$
  - $I(p_{X}, p_{Y|X})$ is concave, but not strictly concave, in $p_{X}$, due to the concavity of the entropy
- Information divergence $D(p || q) = \sum_{a} p(a) \log \frac{p(a)}{q(a)}$
  - Nonnegative, due to Gibbs' inequality
  - Jointly convex in $(p, q)$, due to log-sum inequality
  - Strictly convex in $p$ for a fixed $q$
  - Strictly convex in $q$ for a fixed $p$

### Continuous alphabets

- Differential entropy $h(X) = -\int p(x) \log p(x) dx$
  - Not necessarily nonnegative
  - Not invariant to to coordinate transformation $X = g(S)$
  - Conditional differential entropy $h(X|Y) = \mathbb{E}_{Y}[h(X|Y = y)] = -\int \int p_{X, Y}(x, y) \log p_{X|Y}(x|y) dx dy$
- Mutual information $I(X; Y) = h(X) - h(X|Y)$
  - Nonnegative, due to the nonnegativity of information divergence
  - Invariant to coordinate transformation
- Information divergence $D(p || q) = \int p(x) \log (p(x)/q(x)) dx$
  - Nonnegative, due to Gibbs' inequality
  - Invariant to coordinate transformation
- Information measures for Gaussian distributions
  - $h(X) = \frac{1}{2} \log (2\pi e \sigma^2)$, $h(X) = \frac{1}{2} \log |2\pi e \Lambda|$
  - $h(X|Y) = \frac{1}{2} \log (2\pi e (\lambda_X - \lambda_{XY}^2 / \lambda_Y))$, $h(Y|X) = \frac{1}{2} \log |2\pi e (\Lambda_X - \Lambda_{XY}{\Lambda_X}^{-1} {\Lambda_{XY}}^{\top})|$, 
  - $I(X; Y) = \frac{1}{2} \log (1 - \rho_{XY}^2)^{-1}$, $I(X; Y) = \frac{1}{2} \log |I - B_{XY} B_{XY}^{\top}|^{-1}$
  - $D(p_1 || p_2) = (log e / 2) (\mu_1 - \mu_2)^2 / \sigma^2$, $D(p_1 || p_2) = (log e / 2) (\mu_1 - \mu_2)^{\top}{\Lambda}^{-1} (\mu_1 - \mu_2)$
  - SNR: $(\mu_1 - \mu_2)^2 / \sigma^2$, $(\mu_1 - \mu_2)^{\top}{\Lambda}^{-1} (\mu_1 - \mu_2)$

------

## Information geometry

- Finite alphabet $\mathcal{Y}$ with cardinality $M$
- Each probability distribution: a point in an $M$ dimensional space
- Probability simplex $\mathcal{P}^{\mathcal{Y}}$: $M - 1$ dimensional hyperplane
- Boundary $\partial(\mathcal{P}^{\mathcal{Y}})$ and interior $\mathrm{int}(\mathcal{P}^{\mathcal{Y}})$
- Information divergence $D(p || q)$ on the boundary of the simplex: define $0\log 0 = 0$
- Information projection (I-projection): $p^{*} = \argmin_{p\in \mathcal{P}} D(p || q)$
- Reverse I-projection: $q^{*} = \argmin_{q\in \mathcal{P}} D(p || q)$
- Pythagorean theorem: for concex $\mathcal{P}$, $D(p || q) \ge D(p || p^{*}) + D(p^{*} || q)$
- Linear family $\mathcal{L}$: for $K < M$, for all $i \in [K]$, $\mathbb{E}[t_i(Y)] = \overline{t}_i$
  - In matrix form, $\widetilde{T} p = 0$, i.e., $\mathcal{L}$ is the null space of $\widetilde{T}$
  - $\dim(\mathcal{L}) = M - 1 - K'$, where $K'$ is the rank of $\widetilde{T}$
  - Minimal representation, if $K' = K$, i.e., the rows in $\widetilde{T}$ are linearly independent
  - Closed to linear combinations
  - Pythagorean identity: for $\mathcal{P} = \mathcal{L}$
- Exponential family $\mathcal{E}_{t}(p^{*})$: $q(y) = p^{*}(y)\exp\{x^{\top}t(y) - \alpha(x)\}$
  - all distributions I-projected onto $\mathcal{L}_{t}(p^{*})$ at $p^{*}$ form $\mathcal{E}_{t}(p^{*})$
  - $\mathcal{E}_{t}(p^{*})$ is called the orthogonal family to $\mathcal{L}_{t}(p^{*})$ at $p^{*}$
- ML as reverse I-projection / divergence minimization
  - Type / empirical distribution: $\hat{p}_{Y}(\cdot; y_{1}^{N})$
  - Type identity: $\frac{1}{N} \sum_{i=1}^{N} f(y_n) = \mathbb{E}_{\hat{p}_{Y}(\cdot; y_{1}^{N})} [f(Y)]$
  - $\hat{x}_{\mathrm{ML}} = \argmin_{x} D(\hat{p}_{Y}(\cdot; y_{1}^{N}) || p_{Y}(\cdot; x))$
- EM: complete data $Z$ from $p_{Z}(\cdot; x)$, observation $Y = g(Z)$
  - Nondecreasing likelihood in each iteration due to Gibbs' inequality
  - Expectation: $U(x; \hat{x}^{(n)}) = \mathbb{E}_{p_{Z|Y}(\cdots|y; \hat{x}^{(n)})}[\log p_{Z}(z; x) | Y=y; \hat{x}^{(n)}]$
  - Maximization: $\hat{x}^{(n+1)} = \argmax_{x} U(x; \hat{x}^{(n)})$
  - Advantage: the maximization can be solved analytically for Gaussian mixtures
- Decision form of the data processing inequality (DPI): $D(p_{Z} || q_{Z}) \ge D(p_{Y} || q_{Y})$, with equality iff $p_{Z}(z) / q_{Z}(z) = p_{Y}(g(z)) / q_{Y}(g(z))$
- EM as alternating projections on the probability simplex
  - $\hat{\mathcal{P}}^{\mathcal{Z}}(y_{1}^{N}) = \left\{ \hat{p}_{Z}(\cdot) \in \mathcal{P}^{\mathcal{Z}} : \sum_{z \in  g^{-1}(b)} \hat{p}_{Z}(z) = \hat{p}_{Y}(b; y_1^N), \forall b \in y \right\}$
  - $\hat{p}_{Z}^{*}(\cdot; x) = \argmin_{\hat{p}_{Z} \in \hat{\mathcal{P}}^{\mathcal{Z}}(y_{1}^{N})} D(\hat{p}_{Z} || p_{Z}(\cdot; x)) = p_{Z}(z; x) \hat{p}_{Y}(g(z)) / p_{Y}(g(z); x)$, due to the DPI
  - E-step / I-projection finds the correct empirical distribution from all candidates:
  $\hat{p}_{Z}^{*}(\cdot; \hat{x}^{(n)}) = \argmin_{\hat{p}_{Z} \in \hat{\mathcal{P}}^{\mathcal{Z}}(y_{1}^{N})} D(\hat{p}_{Z} || p_{Z}(\cdot; \hat{x}^{(n)}))$
  - M-step / reverse I-projection:
  $\hat{x}^{(n + 1)} = \argmin_{x} D(\hat{p}_{Z}^{*}(\cdot; \hat{x}^{(n)}) || p_{Z}(\cdot; x))$

------

## Non-Bayesian modeling

### Modeling via mixtures

- Modeling is distinct from estimation even for parametric models
  - Hypothesis testing: decision
  - Estimation: parameter
  - Modeling: distribution
- Modeling via mixtures $q_{w}(y) = \sum_{x\in \mathcal{X}} w(x) p_{Y}(y; x)$
  - For any admissible $q\in \mathcal{P}^{\mathcal{Y}}$, there exists $w(\cdot)$, such that $D(p_{Y}(\cdot; x) || q_{w}(y)) \le D(p_{Y}(\cdot; x) || q(\cdot))$ for all $x\in \mathcal{X}$
- Redundancy-capacity theorem
  - $\max_{x\in \mathcal{X}} D(p_{Y}(\cdot; x) || q(\cdot)) = \max_{w\in \mathcal{P}^{\mathcal{X}}} \sum_{x} w(x) D(p_{Y}(\cdot; x) || q(\cdot))$
  - $C = R^{+} = \min_{q\in \mathcal{P}^{\mathcal{Y}}} \max_{w\in \mathcal{P}^{\mathcal{X}}} \sum_{x} w(x) D(p_{Y}(\cdot; x) || q(\cdot)) = \max_{w\in \mathcal{P}^{\mathcal{X}}} \min_{q\in \mathcal{P}^{\mathcal{Y}}} \sum_{x} w(x) D(p_{Y}(\cdot; x) || q(\cdot)) = R^{-}$
  - The number of $x$ such that $w^{*}(x) > 0$ is at most $|\mathcal{Y}|$: the number of points on the surface of the hyperball that subsumes all $x$
  - Equidistance property: $D(p_{Y}(\cdot; x) || q^{*}) \le C$ for all $x \in \mathcal{X}$, with equality for all $x$ such that $w^{*}(x) > 0$
- Interpret $w = p_{X}$: $q = p_{Y}, R^{-} = \max_{p_{X}} I(X; Y)$
  - Least informative prior for $p_{Y|X}$: $p_{X}^{*} = \argmax_{p_{X}} I(X; Y)$
  - Model capacity of the model $p_{Y|X}$: $C = \max_{p_{X}} I(X; Y)$
  - $0 \le C \le \log |\mathcal{X}|$
- Inference with the optimized mixture model: $w^{*}(x | y_{-}) = \frac{w^{*}(x) L_{y_{-}}(x)}{\sum_{a} w^{*}(a) L_{y_{-}}(a)}$

### Maximally ignorant priors

- Motivation of maximally ignorant priors (MIP): detailed structure of the prior is not critical to good performance & a prior independent of $\mathcal{Y}$
- MIP for finite alphabets
  - Maximum entropy distributions: I-projection of the uniform distribution onto the constraint family
  - For linear constraints via linear family $\mathcal{L}_{t}(p^{*})$: $p^{*}(y) = \exp\{ \sum_{i=1}^{K} x_i t_i(y) - \alpha(x) \}$
- MIP for infinite alphabets
  - For linear constraints, the form of $p^{*}$, when it exists, is the same as that in the case of finite alphabets
  - $\mathbb{E}[Y^2] = \sigma^2$: MIP is $\mathrm{N}(0, \sigma^2)$
  - $p(y) = 0$ for $y < 0$, and $\mathbb{E}[Y] = \mu$: MIP is $\mathrm{Exp}(1/\mu)$

### Conjugate prior families

- Conjugate prior families (CPF) $\mathcal{Q} = \{q(\cdot; \theta): \theta \in \mathbb{R}^{K}\}$: for $y\in \mathcal{Y}$, $p_{X|Y}(\cdot|y) \in \mathcal{Q}$ whenever $p_{X}(\cdot) \in \mathcal{Q}$
  - Equivalently, $p_{X|Y_1, \cdots, Y_N} \in \mathcal{Q}$ whenever $p_{X}(\cdot) \in \mathcal{Q}$
  - Natural CPF: a CPF that has the same form as the model
  - Convex hull of a natural CPF / mixture of natural CPF: unnatural, not an exponential family
- Equivalent statements
  - CPF exists
  - $\exists$ sufficient statistic $t_{N}(y_1, \cdots, y_N)$ for model $p_{Y|X}$ with finite dimension independent of $N$
  - $p_{Y|X}$ is a exponential family with continuous natural statistics
- For model $p_{Y|X}(y|x) = \exp\{ \lambda(x)^{\top} t(y) - \alpha(x) + \beta(y) \}$, the CPF is $\mathcal{Q} = \{q: q(x; t, N) = \exp\{ [t^{\top}\lambda(x) - N \alpha(x)] - \gamma(t, N) \}\}$
  - $N$ is a parameter, not the number of observations
  - The CPF is natural & a linear exponential family
  - The Gaussian family is self-conjugate

*Example.* Beta priors for Bernoulli distributions.
- Gamma function: $\Gamma(z) := \int_{0}^{\infty} u^{z-1} e^{-u} du$ for $z > 0$.
  - $\Gamma(z + 1) = z\Gamma(z)$.
  - For natural number $z$, $\Gamma(z) = (z - 1)!$.
- Beta function: $\Beta(\alpha, \beta) = \int_{0}^{1} x^{\alpha - 1} (1 - x)^{\beta - 1} dx = \Gamma(\alpha) \Gamma(\beta) \Gamma^{-1}(\alpha + \beta)$ for $\alpha, \beta > 0$.
- Beta distribution: $X \sim \mathrm{Beta}(\alpha, \beta)$ for $\alpha, \beta > 0$, if $p_{X}(x) = x^{\alpha - 1} (1 - x)^{\beta - 1} \Beta^{-1}(\alpha, \beta)$.

### Asymptotics of non-Bayesian modeling

- Asymptotics of model capacity
- Universal predictor
- Universal prediction theorem

------

## Approximation

### Stochastic approximation

- Stochastic approximation methods / Monte Carlo methods / sampling methods: construct estimates from data samples
- Importance sampling (IS): modify the approximation $\mathbb{E}_{p}[f(X)]$
  - $w(x) = p_{0}(x) / q_{0}(x)$
  - $\hat{\overline{f}}(x) =  \sum_{i=1}^{n} w(x_i) f(x_i) / \sum_{j=1}^{n} w(x_{j})$
  - $\mathbb{E}_{q}[w(x)] = Z_p / Z_q$: a way to estimate the partition function $Z_p$ if $Z_q$ is known
  - Disadvantage: convergence rate deteriorates as $\mathcal{X}$ or dimension increases
- Rejection sampling (RS): generate i.i.d. samples from $p$
  - Assume a known $c$ such that $cq_{0} > p_{0}(x)$
  - Sample $x$ from $q$, and retain it with probability $p_{0}(x) / (cq_{0}(x))$
  - Acceptance rate: $Z_p / (c Z_q)$
  - Disadvantage: $c$ grows as $\mathcal{X}$ or dimension increases
- Markov chain Monte Carlo (MCMC): asymptotically produce correlated samples from $p$
  - Advantage: viable in high dimensions, the most powerful among sampling methods
  - Idea: construct a reversible, ergodic / irreducible & aperiodic, Markov chain with stationary distribution $p$
- Metropolis-Hastings algorithm: an MCMC method
  - Generate $x'$ from the proposal distribution $V(\cdot|x)$
  - Transit to $x'\neq x$ with probability $a(x\to x') = \min\{ 1, p_0(x') V(x|x') / (p_0(x) V(x'|x)) \}$
  - A local version of rejection sampling: a local $c_{x, x'}$

### Deterministic approximation

------
