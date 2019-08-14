---
layout: post
title:  "Paper notes - Variance-reduced Q-learning is minimax optimal"
date:   2019-07-23 22:00:00 +0800
author: Siberian Tiger
categories: academic
---
Basic References：
Reinforcement Learning: an Introduction, 2nd Edition, by Richard Sutton and Andrew Barto.

> Martin J. Wainwright, [Variance-reduced Q-learning is minimax optimal][wainwright2019variance], 2019.

The focus of this paper is the sample complexity of Q-learning in tabular settings, i.e. MDPs with finite state-action spaces. 

- Episode of length $K$.
- Discount factor $\gamma$.
- Synchronous or generative setting, i.e. simulator assumption: at each iteration, all state-action pairs are executed to observe rewards and new states.  
=> Sample complexity is a factor of $D$ larger than iteration complexity.

## Notations

- The Q-value function:
  $$
  \theta^{\pi}(x, u) :=\mathbb{E}\left[\sum_{k=0}^{\infty} \gamma^{k} r\left(x_{k}, u_{k}\right) \mid x_{0}=x, u_{0}=u\right],
  $$
  where $u_{k}=\pi\left(x_{k}\right)$ for all $k \ge 1$.

- The Bellman Operator is a mapping from $\mathbb{R}^{|\mathcal{X}| \times|\mathcal{U}|}$ to itself, whose $(x, u)$-entry is given by
  $$
  \mathcal{T}(\theta)(x, u) :=r(x, u)+\gamma \mathbb{E}_{x^{\prime}} \max _{u^{\prime} \in \mathcal{U}} \theta\left(x^{\prime}, u^{\prime}\right),
  $$
  where $x^{\prime} \sim \mathbb{P}_{u}(\cdot \mid x)$.

- In RL, the transition dynamics are unknown, so that the Bellman Operator can not be exactly evaluated. This leads to the Empirical Bellman Operator:
  $$
  \widehat{\mathcal{T}}_{k}(\theta)(x, u)=r(x, u)+\gamma \max _{u^{\prime} \in \mathcal{U}} \theta\left(x_{k}, u^{\prime}\right),
  $$
  where the subscript $k$ denotes a random draw.
  Thus, Q-learning is a particular form of stochastic approximation.

## Comparison with related work

- Martin J. Wainwright, [Stochastic approximation with cone-contractive operators: Sharp $\ell_{\infty}$-
bounds for Q-learning][wainwright2019stochastic], 2019: A sample complexity upper bound for ordinary Q-learning is $O(\frac{r_{\max}^2}{\epsilon^2} \frac{D \log(D/\delta)}{(1-\gamma)^4})$, i.e. with probability at least $1-\delta$, the Q-value estimation is $\epsilon$-accurate in $\ell_{\infty}$ norm.

- Azar et al., Minimax PAC bounds on the sample complexity
of reinforcement learning with a generative model, 2013: Model-based Q-iteration has a sample complexity upper bound of $O(\frac{r_{\max}^2}{\epsilon^2} \frac{D \log(D/\delta)}{(1-\gamma)^3})$, and this sample complexity is minimax optimal.

- This paper (**main conclusion**): Variance-reduced Q-learning has a sample complexity upper bound of $O(\frac{r_{\max}^2 D}{\epsilon^2 (1-\gamma)^3} \log(\frac{D}{(1-\gamma) \delta}))$, which reaches the minimax optimal up to a logarithmic factor in the discount complexity factor $1/(1-\gamma)$.

[wainwright2019variance]: https://arxiv.org/abs/1906.04697/

[wainwright2019stochastic]: https://arxiv.org/abs/1905.06265/

## Variance reduction

The ordinary Q-value update is given by 

$$
\theta_{k+1}=\left(1-\lambda_{k}\right) \theta_{k}+\lambda_{k} \widehat{\mathcal{T}}_{k}\left(\theta_{k}\right).
$$

Let $\Delta_{k}=\theta_{k}-\theta^{\star}$ denote the error between the Q-value in the $k$-th iteration and the optimal Q-value. Then the Q-value update can be rewritten as

$$
\Delta_{k+1}=\left(1-\lambda_{k}\right) \Delta_{k}+\lambda_{k}\left\{\widehat{\mathcal{T}}_{k}\left(\theta^{\star}+\Delta_{k}\right)-\widehat{\mathcal{T}}_{k}\left(\theta^{\star}\right)\right\}+\lambda_{k} V_{k},
$$

where $V_{k} :=\widehat{\mathcal{T}}_{k}\left(\theta^{\star}\right)-\mathcal{T}\left(\theta^{\star}\right)$ is a zero-mean random matrix, whose entry-wise variance is called the effective variance in ordinary Q-learning.

The variance can be reduced with the trick of recentering, i.e. substracting a term and then adding another.

$$
\theta \mapsto \mathcal{V}_{k}\left(\theta ; \lambda, \overline{\theta}, \widetilde{\mathcal{T}}_{N}\right) :=(1-\lambda) \theta+\lambda\left\{\widehat{\mathcal{T}}_{k}(\theta)-\widehat{\mathcal{T}}_{k}(\overline{\theta})+\widetilde{\mathcal{T}}_{N}(\overline{\theta})\right\},
$$

where $\overline{\theta}$ is a surrogate for the oracle $\theta^{\star}$, and 
<!-- use single $ below will result bug in MathJax -->
$$\widetilde{\mathcal{T}}_{N}(\overline{\theta}) :=\frac{1}{N} \sum_{i \in \mathfrak{D}_{N}} \widehat{\mathcal{T}}_{i}(\overline{\theta})$$ 
is the Monte Carlo approximation of 
$\mathcal{T}(\overline{\theta})$.
The intuition is that, the variance term vanishes when using the oracle $\theta^{\star}$ and evaluating the Bellman Operator $\mathcal{T}$.

The paper specifies the episode length as $K=c_{1} \frac{\log \left(\frac{8 M D}{(1-\gamma) \delta}\right)}{(1-\gamma)^{3}}$, and the recentering sample size as $N_{m}=c_{2} 4^{m} \frac{\log (8 M D / \delta)}{(1-\gamma)^{2}}$, where $M$ denotes the number of episodes to run and $m$ denotes the episode index.

This recentering trick reduces the $\ell_{\infty}$-norm error decrease geometrically or exponentially. However, the recentering sample size also increases exponentially. The overall effect is the cubic bound in the discount complexity factor $1/(1-\gamma)$.

It seems that this effect is due to the simulator assumption, and is hard to generalize to other settings.

