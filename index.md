---
layout: default
title: Akash Srivastava
---

<!-- <div class="blurb">
	<h1>Akash Srivastava</h1>
	<p>![profile](/profile.jpg) I'm a PhD student in the <a href="http://www.ed.ac.uk/informatics/about/location/forum">Informatics Forum </a>, 
		University of Edinburgh.</p>
	<p>I'm currently working with <a href="http://homepages.inf.ed.ac.uk/csutton/">Dr Charles Sutton</a> 
		on <a href="https://www.cs.princeton.edu/courses/archive/fall11/cos597C/lectures/variational-inference-i.pdf">
		variational inference</a> and <br>interactive machine learning primarily for unsupervised models. </p>
</div><!-- /.blurb --> 


# Akash Srivastava
<img style="float: left;" src="/profile.jpg">I'm a PhD student in the [Informatics Forum](http://www.ed.ac.uk/informatics/about/location/forum), University of Edinburgh.I'm currently working with [Dr Charles Sutton](http://homepages.inf.ed.ac.uk/csutton/) on [neural variational inference](http://akashgit.github.io/Neural-Variational-Inference/) and interactive machine learning primarily for unsupervised models.

---

## Our ICLR 2017 Submission:

---

## 1. [Neural Variational Inference For Topic Models](http://openreview.net/forum?id=BybtVK9lg) || [Code](https://github.com/akashgit/Neural-Variational-Inference-for-Topic-Models)

> #### Authors `Akash Srivastava and Charles Sutton`

#### Abstract

>> Topic models are one of the most popular methods for learning representations 
of text, but a major challenge is that any change to the topic model requires 
mathematically deriving a new inference algorithm. A promising approach to address
this problem is neural variational inference (NVI), but they have proven difficult
to apply to topic models in practice. We present what is to our knowledge the first
effective neural variational inference method for latent Dirichlet allocation (LDA),
tackling the problems caused for NVI by the Dirichlet prior and by component collapsing.
We find that NVI matches traditional methods in accuracy with much better inference
time. Indeed, because of the inference network, we find that it is unnecessary to pay
the computational cost of running variational optimization on test data. Because NVI
is black box, it is readily applied to new topic models. As a dramatic illustration 
of this, we present a new topic model called ProdLDA, that replaces the mixture model
in LDA with a product of experts. By changing only one line of code from LDA, we find
that ProdLDA yields much more interpretable topics, even if LDA is trained via collapsed
Gibbs sampling.

---



