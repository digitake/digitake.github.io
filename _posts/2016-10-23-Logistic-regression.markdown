---
layout: post
title:  "Logistic regression"
date:   2016-10-23 11:27:00 +0700
categories: ml, dl, math, ai
---

Cost function of logistic regression J is a function that is used to minimized 
error(difference) between target output $$y$$ and the result from hypothesis $$h_\theta$$.
$$\theta$$ is a set of parameters. J can be defined as follows: 

$$J(\theta) = -{1 \over m} \bigg[ \sum_{i=1}^m y^{(i)}log(h_\theta (x^{(i)}))+(1-y^{(i)})log(1-h_\theta (x^{(i)})) \bigg] $$

Note that cost function will be computed over all training samples of size $$m$$ whlist $$h(x)$$ is a hypothesis function.
This function is an *approximated* representation of true function that map from $$x \longrightarrow y$$.
 
In order to prevent overfitting we can introduce a "regularization term" to the equation.
Regularization term can be defined as:

$${\lambda \over 2m}\sum_{j=1}^n \theta_j^2$$

such that $$\lambda$$ represents a regularized factor i.e. higher value will reduce the cost variance.
so our cost function with regularization becomes

$$J(\theta) = -{1 \over m} \bigg[ \sum_{i=1}^m y^{(i)}log(h_\theta (x^{(i)}))+(1-y^{(i)})log(1-h_\theta (x^{(i)})) \bigg] + {\lambda \over 2m}\sum_{j=1}^n \theta_j^2$$