---
layout: post
title: "Machine Learning: Trees, bagging and boosting"
date: 2020-10-23
tags: [machine learning]
---

## Bagging

The average of the predictions over a collection of bootstrap samples can reduce variance. This average is a Monte Carlo estimate of the "true" bagging estimates.

![bagging](/assets/img/2020-10-23/bagging1.png){:class="img-responsive"}
[link](https://web.stanford.edu/~hastie/Papers/ESLII.pdf)


## Generalized Additive Models

![gam](/assets/img/2020-10-23/gam1.png){:class="img-responsive"}
[link](https://web.stanford.edu/~hastie/Papers/ESLII.pdf)

![gam](/assets/img/2020-10-23/gam2.png){:class="img-responsive"}
[link](https://web.stanford.edu/~hastie/Papers/ESLII.pdf)

> We fit each function using a scatterplot smoother (e.g., a
cubic smoothing spline or kernel smoother), and provide an algorithm for simultaneously estimating all p functions


