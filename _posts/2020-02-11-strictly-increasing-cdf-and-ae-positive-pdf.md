---
layout: post
title:  "Strictly Increasing CDF Does Not Imply Almost Everywhere Postive PDF"
date:   2020-02-11 18:50:00 -0500
author: Siberian Tiger
categories: math
---

Let $f(x)$ be the probability density function (PDF) of a continuous random variable.
We have the following three statements.
- Statement A: $f(x) > 0$ almost everywhere. As a reminder, 'almost everywhere' means on all real set $\mathbb{R}$ up to a set of measure zero.
- Statement B: For any real numbers $x_1 < x_2$, the Lebesgue integral $\int_{x_1}^{x_2} f(x) ~\mathrm{d}x > 0$.
- Statement C: The cumulative distribution function (CDF) $F(x) = \int_{-\infty}^{x} f(x) ~\mathrm{d}x$ is strictly increasing.

The question is, what the relationships between the three statements are.

Obvious relationships:
1. Statement B and Statement C are equivalent. This is trivially because for any real numbers $x_1 < x_2$, $F(x_2) - F(x_1) = \int_{x_1}^{x_2} f(x) ~\mathrm{d}x > 0$.
2. Statement A implies Statement B. This is because $\mu((x_1, x_2)) = x_2 - x_1 > 0$, where $\mu(\cdot)$ denotes the Lebesgue measure.

It remains to be determined whether Statement B implies Statement A, so that all three statements are equivalent. 
However, the answer is negative. We provide an example here to show that Statement A is strictly stronger than Statement B.

To prepare the readers for our argument, we invite the readers to recall the following facts. Note that whenever we talk about 'measurable' or 'integrable' in the sequel, we always mean in the Lebesgue sense, even if we do not mention 'Lebesgue' explicitly.

- Fact 1: The Smith–Volterra–Cantor set (SVC set) is a closed set on the real line, which has a positive meansure of $1/2$, and yet contains no open intervals.
- Fact 2: The indicator functions of a measurable set is measurable.
- Fact 3: A function $\mathbb{R}\mapsto \mathbb{R}$ is a PDF, if it is non-negative almost everywhere and its Lebesgue integral on the real set is $1$.
- Fact 4: Lebesgue measurable functions are closed under multiplication.
- Fact 5: Let $f$ be a bounded measurable function on a set of finite measure. Then, $f$ is Lebesgue integrable over the set.
- Fact 6: Lebesgue integrable functions are closed under addition. In fact, Lebesgue integrable functions form a linear space.
- Fact 7: An open set minus a closed set is an open set.
- Fact 8: The Lebesgue measure of a measurable open set on the real line is positive.
- Fact 9: The Lebesgue integral of a positive function on a set of positive measure is positive.

Now we are ready to begin our argument.
Let $g$ be a bounded PDF that is positive everywhere, e.g., a PDF of a Gaussian distribution. 
Let $\mathcal{S}$ denote the SVC set.
Define a new function $\hat{f}$ such that $\hat{f}(x) = g(x)$ if $x \notin \mathcal{S}$ and $\hat{f}(x) = 0$ if $x \in \mathcal{S}$.

We claim that $\hat{f}$ is Lebesgue integrable.
The proof is as follows.
Let $I_{\mathcal{S}}$ be the indicator function of the SVC set $\mathcal{S}$, i.e., $I_{\mathcal{S}}(x) = 1$ if $x \in \mathcal{S}$ and $I_{\mathcal{S}}(x) = 0$ otherwise.
Because $\mathcal{S}$ is Lebesgue measurable (Fact 1), the indicator function $I_{\mathcal{S}}$ is Lebesgue measurable (Fact 2).
The PDF $g$ is Lebesgue integrable by definition (Fact 3) and is certainly Lebesgue measurable.
Therefore, the pointwise multiplication $g \cdot I_{\mathcal{S}}$ is Lebesgue measurable (Fact 4).
Since $g \cdot I_{\mathcal{S}}$ is bounded, it is integrable on $\mathcal{S}$ (Fact 5) and thus on $\mathbb{R}$.
Essentially, $\hat{f} = g - g \cdot I_{\mathcal{S}}$, and thus $\hat{f}$ is also Lebesgue integrable (Fact 6).

We proceed to show that for any real numbers $x_1 < x_2$, the Lebesgue integral $\int_{x_1}^{x_2} \hat{f}(x) ~\mathrm{d}x > 0$.
Since $(x_1, x_2)$ is an open interval and $\mathcal{S}$ is a closed set (Fact 1), $(x_1, x_2) \backslash \mathcal{S}$ is an open set (Fact 7), where '$\backslash$' denote set substraction.
Therefore, $\mu((x_1, x_2) \backslash \mathcal{S}) > 0$ (Fact 8), and $\int_{x_1}^{x_2} \hat{f}(x) ~\mathrm{d}x > 0$ (Fact 9).

Specifically, $0 < \int_{-\infty}^{\infty} \hat{f}(x) ~\mathrm{d}x = I \le 1$.
Now define $f = \hat{f} / I$.
Then $f$ is a valid PDF (Fact 3),
which satisfies Statement B, and yet does not satisfy Statement A, because $f$ is zero on $\mathcal{S}$, a set of positive measure.

In conclusion, Statement A $\Rightarrow$ Statement B $\Leftrightarrow$ Statement C, and Statement B $\nRightarrow$ Statement A.
