---
layout: default
title: Akash Srivastava
---

<!-- <div class="blurb">
	<h1>Akash Srivastava</h1>
	<p>![profile](/profile.jpg) I'm a PhD student in the <a href="http://www.ed.ac.uk/informatics/about/location/forum">Informatics Forum </a>, 
		University of Edinburgh.</p>
	<p>I'm currently working with <a href="http://homepages.inf.ed.ac.uk/csutton/">Dr Charles Sutton</a> 
		on <a href="https://www.cs.princeton.edu/courses/archive/fall11/cos597C/lectures/variational-inference-i.pdf"> ![profile](/profile.jpg)  <img style="float: left;" src="/profile.jpg">
		variational inference</a> and <br>interactive machine learning primarily for unsupervised models. </p>
</div><!-- /.blurb --> 

<img style="float: right;" src="/profile.jpg">

#   Akash Srivastava

I'm a PhD student in the [Informatics Forum](http://www.ed.ac.uk/informatics/about/location/forum), University of Edinburgh. Currently, I'm working with [Dr Charles Sutton](http://homepages.inf.ed.ac.uk/csutton/) on [autoencoding variational inference](http://akashgit.github.io/Neural-Variational-Inference/) and [interactive machine learning](https://arxiv.org/abs/1602.06886v1) primarily for unsupervised models.

---

## New ICLR 2017 Paper: *Title Updated*

---

## 1. [Autoencoding Variational Inference For Topic Models](http://openreview.net/forum?id=BybtVK9lg) || [Code](https://github.com/akashgit/Neural-Variational-Inference-for-Topic-Models)

> #### Authors `Akash Srivastava and Charles Sutton`

#### Abstract

>> Topic models are one of the most popular methods for learning representations of
text, but a major challenge is that any change to the topic model requires mathematically
deriving a new inference algorithm. A promising approach to address
this problem is autoencoding variational Bayes (AEVB), but it has proven diffi-
cult to apply to topic models in practice. We present what is to our knowledge the
first effective AEVB based inference method for latent Dirichlet allocation (LDA),
which we call Autoencoded Variational Inference For Topic Model (AVITM). This
model tackles the problems caused for AEVB by the Dirichlet prior and by component
collapsing. We find that AVITM matches traditional methods in accuracy
with much better inference time. Indeed, because of the inference network, we
find that it is unnecessary to pay the computational cost of running variational
optimization on test data. Because AVITM is black box, it is readily applied
to new topic models. As a dramatic illustration of this, we present a new topic
model called ProdLDA, that replaces the mixture model in LDA with a product
of experts. By changing only one line of code from LDA, we find that ProdLDA
yields much more interpretable topics, even if LDA is trained via collapsed Gibbs
sampling.

---



