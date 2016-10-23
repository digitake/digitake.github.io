---
layout: post
title:  "Logistic regression"
date:   2016-10-23 11:27:00 +0700
categories: ml, dl, math, ai
---

When $$a \ne 0$$, there are two solutions to \(ax^2 + bx + c = 0\) and they are
$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

Cost function of logistic regression J is a function that is used to minimized 
error(difference) between target output $$y$$ and the result from hypothesis $$h_\theta$$.
$$\theta$$ is a set of parameters. J can be defined as follows: 

$$J(\theta) = -{1 \over m} \sum_{i=1}^m y^{(i)}log(h_\theta (x^{(i)}))+(1-y^{(i)})log(1-h_\theta (x^{(i)})) $$ 