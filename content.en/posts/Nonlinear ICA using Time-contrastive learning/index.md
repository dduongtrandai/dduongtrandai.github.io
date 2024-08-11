---
author: "duongtd"
date: 2024-07-31
title: Nonlinear ICA using Time-contrastive learning
tags: ["ICA", "NonlinearICA"] 
categories: ["Statistics"]
params:
  math: true
---
* We learn features that enable discriminating data points from different time segments
* We use ordinary neural network training:
  Last hidden layer gives the features
* Surprising theoretical result:
  Estimates a nonlinear ICA model
  * with general nonlinear mixing $x(t) = f(s(t))$
  * **nonstationary** components $s_{i}(t)$
