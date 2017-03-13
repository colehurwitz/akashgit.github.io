---
layout: post
title: "Unsaturating Softmax"
date: 2017-03-13
---

## Unsaturating Softmax

The softmax function is a multi-dimensional extension to the sigmoid function that projects an incoming vector to a unit simplex. Therefore it is quite frequenly used in logistic regression (classification) tasks to represent a multinomial distribution over the data classes.

Mathematically, it is represented as $$\sigma(x_i)=\frac{e^{x_i}}{\sum_j e^{x_j}}$$. 
