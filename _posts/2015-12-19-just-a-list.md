---
layout: post
title: "Just a List"
date: 2015-12-19
---
I finally figured out how to use [KaTex](https://github.com/Khan/KaTeX) last night and posted a something on the gradient of logistic regression to test things out.
So now I've decided to maintain this list of mathematical words/jargons that I come across quite frequently in my field and everytime have to check wikipedia to refresh my memory. I hope this will make it easier for me to remember them. 

**Subadditive:**
A subadditive function is a function $$f:A \rightarrow B$$ , having a domain A and an ordered codomain B that are both closed under addition, with the following property,

$$ \forall x,y \in A, f(x+y) \leq f(x) + f(y) $$

**Submodular:**
Let $$N$$ be a finite ground set and $$ f : 2^{N} \to R $$. Then $$f$$ is submodular if $$\forall A,B \subseteq N$$,

$$f(A) + f(B) \geq f(A \cup B) + f(A \cap B)$$


**Hamming Distance:**
In information theory, the Hamming distance between two strings of equal length is the number of positions at which the corresponding symbols are different

**Log Determinant of SPD Matrix**
Usually in computation packages the determinant of the covariance matrix throws __NaNs__ . But it turns out that __log__ of the determinant might still be finite. Therefore,

`L = tf.tf.cholesky(cov)`

`log_det_cov = 2*reduce_sum(tf.log(tf.matrix_diag(L)))`
