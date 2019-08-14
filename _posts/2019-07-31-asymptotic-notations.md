---
layout: post
title:  "Asymptotic Notations"
date:   2019-07-31 21:53:00 +0800
author: Siberian Tiger
categories: academic
---
Asymptotic notations play an important role in mathematics and computer science. 
The $O, \Omega, \Theta, o, \omega$ notations are also collectively referred to as the family of Bachmann–Landau notations, named after the inventors.

1.  Big O notation. $f(x) = O(g(x))$ iff there exists a positive real number $M$ and a real number $x_0$ such that 
    
    $$
    |f(x)| \leqslant M g(x), \quad \forall x \geqslant x_{0}.
    $$
    
    Its equivalent limit definition is given by
    
    $$
    \lim _{x \rightarrow \infty} \sup \left|\frac{f(x)}{g(x)}\right|<\infty.
    $$
    
    It reads 'f(x) is big O of g(x)'. 'O' comes from 'order' of functions.

    Big O notation indicates an upper bound. 
    In some contexts like partial differential equations and harmonic analysis, it is also written as $f(x) \lesssim g(x)$.

    A derived notation from big O is the soft O notation $\tilde{O}$, which ignores logarithmic factors, i.e. 
    
    $$
    f(x) = \tilde{O}(g(x)) \iff f(x) = O(g(x) \log^k g(x)),
    $$
    
    where $k > 0$.


2.  Big Omega notation in complexity theory by Knuth. The limit definition: $f(x) = \Omega(g(x))$ iff
    
    $$
    \lim _{x \rightarrow \infty} \inf \left|\frac{f(x)}{g(x)}\right|>0.
    $$
    
    Big Omega indicates a lower bound, and it is essentially the dual notation of big O, i.e.
    
    $$
    f(x) = O(g(x)) \iff g(x) = \Omega(f(x)).
    $$

    In number theory, big Omega notation has a different meaning, where the $\inf$ becomes $\sup$.

3.  Big Theta notation. $f(x) = \Theta(g(x))$ iff there exist two positive real numbers $k_1$ and $k_2$ and a constant $x_0$ such that
    
    $$
    k_1 g(x) \leqslant f(x) \le k_2 g(x), \quad \forall x \geqslant x_0.
    $$
    
    Big Theta indicates the same order. Another definition for it is given by
    
    $$
    f(x) = \Theta(g(x)) \iff f(x) = O(g(x)) \text{ and } f(x) = \Omega(g(x)).
    $$

    A special case of big Theta is when 
    
    $$
    \lim _{x \rightarrow \infty} \frac{f(x)}{g(x)}=1.
    $$
    
    In this case, we say that $f(x)$ is on the order of $g(x)$, with the new notation $f(x) \sim g(x)$.

4.  Small o notation. $f(x) = o(g(x))$ iff for every positive constant $\varepsilon$, there exists a constant $N$ such that
    
    $$
    |f(x)| \leqslant \varepsilon g(x), \quad \forall x \geqslant N.
    $$
    
    Its equivalent limit definition is given by
    
    $$
    \lim_{x\rightarrow \infty}\frac{f(x)}{g(x)} = 0.
    $$

5.  Small omega notation. The limit definition: $f(x) = \omega(g(x))$ iff 
    
    $$
    \lim _{x \rightarrow \infty}\left|\frac{f(x)}{g(x)}\right|=\infty.
    $$
    
    Small omega is essentially the dual notation of small o, i.e.
    
    $$
    f(x) = o(g(x)) \iff g(x) = \omega(f(x)).
    $$
