---
layout: post
title: Unexpected behaviours of expectations
date: 2023-04-23 00:00:00-0000
description: Averaging and times when it can go wrong
tags: math stats
categories: 
related_posts: false
---
The average/mean/expectation is perhaps the most known and commonly used statistical estimator. We tend to use it when we want to estimate the `location` of the distribution - its centre.

Most often when faced with a set of values (samples) `$x_1,x_2, ... , x_n$` (representing instantiations of a random variable `$X$`) we can estimate the expectation as `$\mathbb{E}(X) = \frac{1}{n}\sum_{i=1}^{i=n} x_i$`.

When we assume that `$X$` is a Gaussian (Normal) distribution, `$X \sim Normal(\mu,\sigma^2) = \frac{1}{\sigma \sqrt(2 \pi)} exp(-(x-\mu)^2/\sigma^2)$` the expectation is the mean $\mathbb{E}(X) = \mu$.

If we were to repeat the experiment, drawing values `$x_1,...x_n$` multiple times, we would find that our estimate $\mu$ - caused by the (assumed) randomness  of the sampling process. The uncertainty of our estimate, the `standard error` is determined by the spread (the standard deviation $\sigma$) of the distribution:

$$\sigma_\mu = \frac{\sigma}{\sqrt{n}}$$

Thus our uncertainty in estimating `$\mu$` scales as `$O(n^{-1/2})$`, meaning that to shrink the uncertainty in the mean by a factor of `$\times 10$` we need to sample `$n\times100$` values. While merely a curiosity here, we will delve deeper in future posts where this expression will appear in the context of numeric integration using Monte Carlo and Quasi-Monte Carlo methods where we will answer the question "Can we achieve a faster rate converge faster than $O(n^{-1/2})" with a "Yes!".

Here we will however consider a few things that can go wrong - when does averaging not give us the correct result? 

# Non-symmetric distributions



# Outliers and breakdown points

So ok, we can't hope to get good mean estimators by simple averaging when our distribution is non-symmetric. But surely if our distribution is symmetric and we average long enough - our mean will converge to a value right? Not quite.

Consider what happens when we replace one of the samples $x_i = \infty$. When we compute the mean we get $\mu = \infty$ - the infinity propagates straight through our sum and causes trouble in $\mu$.

What we did here is make our estimator infinitely large by changing a single value - we could have changed more. From this we can introduce the concept of a `breakdown point` - the number of infinities that our estimator can handle before it is affects. From above it one can see that the traditional mean has a breakdown point of 0.

What are some other estimators for the location that are `robust` to outliers you might ask? Good question - the median is one. This has a breakdown point of 50% (or 0.5) - meaning that the median can tolerance up to 50% of the samples being corrupted (ie. $\pm \infty$) before it is affected.

# Pathological distributions - the Gaussian assumption

Related to the above discussion of outliers is the assumption that the distribution is Gaussian. A key feature of the Gaussian is that it's probability density decayed quadratically (the log of the density is a parabola).

While the assumption that a distribution is Gaussian is useful, it may not hold in practice - symmetric distributions for which the mean is undefined exist!

## Cauchy distribution 

<!-- 
This theme supports rendering beautiful math in inline and display modes using [MathJax 3](https://www.mathjax.org/) engine. You just need to surround your math expression with `$$`, like `$$ E = mc^2 $$`. If you leave it inside a paragraph, it will produce an inline expression, just like $$ E = mc^2 $$.

To use display mode, again surround your expression with `$$` and place it as a separate paragraph. Here is an example:

$$
\sum_{k=1}^\infty |\langle x, e_k \rangle|^2 \leq \|x\|^2
$$

You can also use `\begin{equation}...\end{equation}` instead of `$$` for display mode math.
MathJax will automatically number equations:

\begin{equation}
\label{eq:cauchy-schwarz}
\left( \sum_{k=1}^n a_k b_k \right)^2 \leq \left( \sum_{k=1}^n a_k^2 \right) \left( \sum_{k=1}^n b_k^2 \right)
\end{equation}

and by adding `\label{...}` inside the equation environment, we can now refer to the equation using `\eqref`.

Note that MathJax 3 is [a major re-write of MathJax](https://docs.mathjax.org/en/latest/upgrading/whats-new-3.0.html) that brought a significant improvement to the loading and rendering speed, which is now [on par with --> KaTeX](http://www.intmath.com/cg5/katex-mathjax-comparison.php).
