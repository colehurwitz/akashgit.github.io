---
layout: default
title: Research
---

## 1. [Neural Variational Inference For Topic Models] (http://openreview.net/forum?id=BybtVK9lg)

### [Code] (https://github.com/akashgit/Neural-Variational-Inference-for-Topic-Models)

### Author `Akash Srivastava and Charles Sutton`

### Abstract

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

## 2. [Clustering with a Reject Option: Interactive Clustering as Bayesian Prior Elicitation] (https://arxiv.org/abs/1602.06886)

### Author `Akash Srivastava, James Zou, Ryan P. Adams and Charles Sutton`

### Abstract

>> A good clustering can help a data analyst to explore and understand a data set, 
but what constitutes a good clustering may depend on domain-specific and application
 specific criteria. These criteria can be difficult to formalize, even when it is easy 
for an analyst to know a good clustering when she sees one. We present a new approach 
to interactive clustering for data exploration, called TINDER, based on a particularly simple
feedback mechanism, in which an analyst can choose to reject individual clusters and 
request new ones. The new clusters should be different from previously rejected clusters
while still fitting the data well. We formalize this interaction in a novel Bayesian prior
elicitation framework. In each iteration, the prior is adapted to account for all the 
previous feedback, and a new clustering is then produced from the posterior distribution.
To achieve the computational efficiency necessary for an interactive setting, we propose 
an incremental optimization method over data minibatches using Lagrangian relaxation. 
Experiments demonstrate that TINDER can produce accurate and diverse clusterings.

---

## 3. [Burst Detection Modulated Document Clustering: A Partially Feature-Pivoted Approach To First Story Detection] (http://project-archive.inf.ed.ac.uk/msc/20141611/msc_proj.pdf)

### Author `Akash Srivastava`

### Abstract 

>> First Story Detection or FSD is one of the 5 tasks defined under the Topic Detection andTracking program with the purpose to identify the onset of a previously unseen event in
a stream of news stories. In this work, we report on the development and evaluation of
a feature-pivoted approach to this task. Our method uses the output of a burst detection
algorithm to modulate the traditional document clustering based approach to FSD.
For burst detection, we work exclusively with words in the input and use a 2 step
filtration routine that filters out all the words for which the cumulative term frequencies
or the Autocorrelation values of their corresponding signal representations are below
a pre-computed threshold. The output is then grouped into sets of words that have
similar burst patterns in time. A confidence score is generated for each set of words,
quantifying the chance of the set being the first story on the event that it relates to. In
the final step all the detected first stories are passed through a restricted clustering unit
that uses cosine similarity to cluster together stories that are on the same topic, hence
reducing false alarms. Our experiments show that the resultant FSD system performs
substantially better than the document-pivoted state-of-art baseline system.

---
