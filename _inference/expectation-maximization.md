---
title: "Expectation Maximization Algorithm"
date: 2017-04-02 20:41:49.00 +01:00
---

## Introduction

The EM algorithm has been created to obtain the MLE in presence of missing data. Imagine that we are interested in estimate $\theta$ using the log-likelihood function $l(\theta; x, y)$; where the realizations $y$ are not available. In that case, the idea of the `EM` algorithm is to:

- *Expectation step*:Estimate the log-likelihood $l(\theta; x, y)$ by obtaining the expected value of the log-likelihood with respect to the conditional distribution of $Y$ given $x$ and for a fixed value of $\theta^*$.
- *Maximization step*: Maximize the estimated value of the log-likelihood with respect to $\theta$ to obtain a new $\theta^*$ for next iteration.
- Iterate until convergence.

It can be shown that the log-likelihood $l(\theta;x)$ is non-decreasing in each iteration of the `EM` algorithm. It worths mention that it is mainly used for maximizing the likelihood function when its expression is easiest to evaluate with an additional data $y$.

## Standard Errors

It is known that asymptotically the MLE $\hat{\theta}$ is normally distributed with mean $\theta_0$ and variance $I_E(\theta_0)^{-1}$, where $\theta_0$ represents the true value of $\theta$. Two alternatives can be used for the covariance matrix $I_E(\hat{\theta})^{-1}$, $I_O(\hat{\theta})^{-1}$ because $\theta_0$ is unknown. Then, in order to compute the standard error of the estimator, the inverse of the observed information is required.

For one parameter case, it can be shown that:

$-\frac{d^2}{d\theta^2} log f(x|\theta) = - \frac{\partial^2 Q(\theta, \phi)}{\partial\theta^2} - - \frac{\partial^2 H(\theta, \phi)}{\partial \theta^2}$
where $Q$ is just the estimated log-likelihood obtained from the *expectation step* and $H$ is the variance of the derivative of the logarithm of $f(x, Y, \theta)$ for fixed values $x$ and $\hat{\theta}$.


<!-- ## Example -->

<!-- ### Description -->

<!-- ### R Implementation -->

## References

- Computational Intensive Methods, Lancaster University

