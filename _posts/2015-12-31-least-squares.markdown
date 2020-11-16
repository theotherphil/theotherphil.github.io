---
layout: post
title:  "Least squares as maximum likelihood"
date:   2015-12-31 21:11:00 +0000
---

<script type="text/javascript" id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-svg.js">
</script>

When fitting a model it's common to choose parameters to minimise the sum of squared errors on the training data.

>**Definition**
>Given training data \\(\mathcal{D}=\lbrace(x_i, y_i)\rbrace_{i=1}^n\\) with \\(x_i \in \mathbb{R}^p\\), \\(y_i \in \mathbb{R}\\) and a model \\(f(x; \theta)\\), the least squares estimator for \\(\theta\\) is that which minimises \\(\Sigma_{i=1}^n(f(x_i; \theta) - y_i)^2\\).

Why minimise the sum of squares, rather than any of several other sensible error functions? For example, why not choose \\(\theta\\) to minimise the sum of absolute errors \\(\Sigma_{i=1}^n\|f(x_i; \theta) - y_i\|\\)? A practical justification is that the squaring function is differentiable, and therefore easy to minimise. A theoretical justification is provided by the following proposition.

>***Proposition***
>Suppose given data \\(\mathcal{D}=\lbrace(x_i, y_i)\rbrace_{i=1}^n\\), where $$y_i = f(x_i; \theta) + \epsilon_i$$ with independent \\(\epsilon_i \sim \mathcal{N}(0, \sigma^2)\\). The least squares estimator for \\(\theta\\) is equal to the maximum likelihood estimator.

In other words, if we assume that the data we're given really were generated according to our model, but that our observations of the \\(y_i\\) suffered from Gaussian measurement errors, then the least squares estimator for the model parameters is also that with maximum likelihood.

To see why, consider the likelihood function:

$$
\begin{align}
L(\theta|\mathcal{D})
    &= P\left(
        \bigwedge_{i=1}^n f(x_i; \theta) + \epsilon_i = y_i
        \right) \\
    &= \Pi_{i=1}^n P\left(
        f(x_i; \theta) + \epsilon_i = y_i
        \right) \\
    &= \Pi_{i=1}^n
        \frac{1}{\sigma\sqrt{2 \pi}}
        \exp\left(
            -\frac{1}{2}\left(\frac{f(x_i; \theta) - y_i}{\sigma}\right)^2
        \right).
\end{align}
$$

As log is monotonically increasing, maximising the likelihood is equivalent to maximising

$$
\begin{align}
\log L(\theta|\mathcal{D})
    &= \log\left(
            \Pi_{i=1}^n
                \frac{1}{\sigma \sqrt{2 \pi}}
                    \exp\left(
                        -\frac{1}{2}\left(\frac{f(x_i; \theta) - y_i}{\sigma}\right)^2
                    \right)
        \right) \\
    &= K - \frac{1}{2 \sigma^2} \Sigma_{i=1}^n \left(f(x_i; \theta) - y_i\right)^2.
\end{align}
$$

Here \\(K\\) is negative and independent of \\(\theta\\). Computing the maximum likelihood estimator therefore reduces directly to least squares.
