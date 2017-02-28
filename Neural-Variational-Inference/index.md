---
layout: default
comments: true
title: "Blackbox and Approximate Neural Inference"
---
# Blackbox and Approximate (Variational) Neural Inference 
For quite sometime now I've been working on neural inference methods that have become very popular recently. There is an abundance of resources on these methods and that is precisely why I decided to write a considerably terse post about the most prominent of such techniques. Since this is only an attempt to summarize the vast body of work being done in this field, I will try to provide links to more detailed (read: much better than mine) posts and paper for each of the methods. As mentioned earlier, this is only an attempt to summarize this fairly sophisticated field, please correct me via the comments section at the end of this page if you find any mistakes in my description, of which I can promise there will be plenty to fix :) Lastly before starting, this is more of a *dynamic* post, meaning that I will keep updating the entries and adding details as I get time.

With that lets delve straight into our main topic, __Approximate Neural Inference__ or as we will refer to it throughout this text, __NI__. Simply put, variational inference (__VI__) is a deterministic method of carrying out approximate inference in probabilistic models when the posterior distribution over the variables of interest (or the latent state) is intractable. In order to do so, VI uses a tractable family of distributions to approximate the intractable posterior in an optimization procedure that usually minimizes the negative log-likelihood of the data that the model is trying to fit. Consider the following example,

<div class="roundedBorder">
<h2 class="c"> Update: <a href="http://homepages.inf.ed.ac.uk/imurray2/">Dr Iain Murray</a> has a nice self-contained stochastic variational inference demo in Matlab/Octave available <a href="http://www.inf.ed.ac.uk/teaching/courses/mlpr/2016/notes/svi_minimal.m">here</a>. Also check out <a href="http://people.seas.harvard.edu/~dduvenaud/papers/blackbox.pdf"> this paper</a> by <a href="https://www.cs.toronto.edu/~duvenaud/">David Duvenaud</a> and <a href="http://people.seas.harvard.edu/~rpa/">Ryan P. Adams</a> for a very short (5-lines) Python based example of blackbox stochastic variational inference.</h2>.
</div>

### Example

Let $$p_\Theta(x)=\int_zp(x\vert z,\alpha)p(z\vert \beta)dz$$ be the likelihood of our data $$x$$ under our model parameterized by $$\Theta=\{\alpha,\beta\}$$ where $$z$$ (continuous or discrete in which case $$\int$$ can be replaced by $$\sum$$) is a latent variable. Assuming, the posterior distribution $$p_\theta(z\vert x)$$ is intractable, mean-field VI (which is a type of VI) approximates this posterior by first introducing variational parameters $$\phi$$ for each $$z$$ and then approximate the true posterior $$p_\theta(z\vert x)$$ by the variational posterior $$q_\phi(z\vert x)$$. In practice, instead of directly optimizing the negative log-likelihood to fit the posterior, VI methods use a simpler to optimize lowerbound on it (popularly referred to as the __ELBO__ or the evidence lowerbound). Traditional VI methods make use of *conjugate* priors over the latent variables to derive closed form `EM-like` updates for optimization, which accounts for their fast speed of inference. But this is also the reason for their limited applicability and/or accuracy. Not all models can leverage the convenience of conjugate priors. Another drawback is the need of repeated derivations for even minor changes in initial assumptions. __NI__ can be thought of as an alternative form or approximate varitational inference that has a certain *black-box* characteristic to it and therefore allows for carrying out approximate inference without the need to derive update equations even in the models that do not have conjugate priors. 

I think that is all that we need to know from traditional VI theory to proceed further. The only other thing that needs to be spelled out is the actual __ELBO__ that is optimized in the old methods can be written down in two equivalent ways as follows,

$$\log p_\Theta(x)\geq
\log p_\Theta(x)-D_{KL}[q_\phi(z\vert x)\vert \vert p_\theta(z\vert x)]$$

$$=
E_{z \sim q}[\log p_\alpha(x\vert z)]-D_{KL}[q_\phi(z\vert x)\vert \vert p_\beta(z)]$$.

---

## 1. Variational Autoencoder (VAE) 

##### `Kingma and Welling, 2013`

VAE uses the following ELBO, $$E_{z \sim q}[\log p_\alpha(x\vert z)]-D_{KL}[q_\phi(z\vert x)\vert \vert p_\beta(z)]$$. Where within the KL term instead of using the posterior $$p_\theta(z\vert x)$$ it regularizes the variational posterior by the prior $$p_\beta(z)$$ over $$z$$.The benefit of this change is that unlike the (intractable) posteriors, priors are always available in Bayesian methods. The problematic term is the expectation over the log conditional of the data $$\log p_\alpha(x\vert z)$$. While this expectation cannot always be computed, it can always be approximated using *Monte-Carlo* (__MC__) given we can sample from the variational posterior. Considering that is true for at least some exponential family distributions we can therefore estimate the EBLO.

VAEs use a feed-forward neural network, called the *inference network* for generating the parameters $$\phi$$ of the variational posterior and a *recognition network* for decoding the data. Using an inference network for generating variational distribution imposes a certain smoothness assumption over the data-points and hence instead of having a mean-filed type local parameters, the network allows sharing of global variational parameter. Training this network is problematic because by using MC for approximating the expectation in the above ELBO, discontinuity is introduced in the graph and hence back propagation is not possible. Back propagating through random sampler is a well studied problem and the way VAE solve it is by using the __reparametrization trick__/__Mat-trick__ which is applicable to any continuous distribution that has a __non-centered parametric form__. I do not want to get in detail of these tricks here as that would require a lot more space than I have, so I will finish this description of VAEs by saying that VAEs can be used as a __neural inference__ method for a large class of continuous latent state model where the prior over the latent variable has a __non-centered parametric form__. Recently, we also showed that VAEs can be used for __Dirichlet__ priors like in a topic model using __Laplace Approximation__. Details can be found [here](http://openreview.net/forum?id=BybtVK9lg). In future I will update this section for the more recent stuff such as,

#### 1.1 Normalizing Flows and Beyond

So what if your posterior is not a unimodal Gaussian distribution? This is the type of issue that Normalizing Flows and related methods are trying to resolve. The basic idea is fairly simple, lets assume that your complicated posterior is some complicated transformation of unimodel Gaussian. So Normalizing flows essentially uses special invertible functions (__such that the determinant of the Jacobian of their inverse is known__) to transform the unimodal Gaussian to approximate your complicated posterior well. More on this later, but for now note that there are several ways to go about using the same idea, including but not limited to __volume preserving transformations__, __invertible neural networks__, etc. 

#### 1.2 Component Collapsing in VAEs and Training Tricks

We are releasing an extended version of our ICLR paper to explain in point in further mathematical detail.

#### 1.3 Using VAEs to Infer LDA-type Topic Models

<div class="roundedBorder">
<h2 class="c"> We recently released the code for <a href="http://openreview.net/pdf?id=BybtVK9lg">Nueral Variational Inference for Topic Models</a> available <a href="https://github.com/akashgit/Neural-Variational-Inference-for-Topic-Models">here</a>. </h2>
</div>
.

#### 1.4 Implementation

While there are plenty of VAE implentations all over the web in almost every Deep Learning package I find [this](https://jmetzen.github.io/2015-11-27/vae.html) `Tensorflow` implementation by Jan Hendrik Metzen quite intuitive and easy to follow. 


---

## 2. Neural Variational Inference Learning 

##### `Mnih and Gregor, 2014`

NVIL is a more general method of inference that is equally applicable to both continuous and discrete latent state probabilistic models. Lets start by considering how the ELBO is transcribed as an expectation in NVIL by absorbing the prior over $$z$$ into the joint of the model,

$$L(x,\Theta,\phi)=E_{z \sim q}[\log p_\Theta(x, z) - \log q_\phi(z\vert x)]$$

Like VAEs, in NVIL the variational posterior $$q_\phi(z\vert x)$$ is constructed using an inference network as well. The gradients of this ELBO *w.r.t* to $$\Theta$$ and $$\phi$$ are given as follows,

$$\nabla_\Theta L(x) = E_{z \sim q}[\nabla \log p_\Theta(x, z)]$$ and 

$$\nabla_\phi L(x) = E_{z\sim q}[(\log p_\Theta(x, z) - \log q_\phi(z\vert x)). \nabla_\phi \log q_\phi(z\vert x)]$$.

There is no problem with approximating $$\nabla_\Theta L(x)$$ with MC but the high variance in the MC approximation of $$\nabla_\phi L(x)$$ requires additional methods to train successfully. To this end, the authors proposed two black-box methods of variance reduction in the gradient estimates. $$(\log p_\Theta(x, z) - \log q_\phi(z\vert x))$$ is called the __learning signal__.

#### 2.1 Centering the Learning Signal

The reason that the gradient with respect to $$\phi$$ is written as an expectation (by clever use of log-derivative trick and moving differentiation operator in and out of summation) is to allow substracting from the learning signal, any quantity that does not depend on $$z$$. Since expectation in the learning signal remains invariant if a quantity $$c$$ is subtracted from it, therefore, a systematically calculated function of the data, $$C(x)$$ when subtracted from the learning signal can help bring the noise down in the gradients. 

#### 2.2 Variance Normalization

While centering the learning signal reduces the variance in the gradients, it does not suffice just by itself as the gradients tend to have shift drastically at times. Therefore, the variance of the learning signal is used to further normalize the gradients.

<div class="roundedBorder">
<h2 class="c"> Update: We have been recently exploring NVIL type methods to more fundamentally explain and resolve the cause of high variance without needing to change the gradients, which also allows faster training in the inference network. Manuscript in preparation. </h2>.
</div>

NVIL also allows benefiting from the local structure of the model.

#### 2.3 Implementation

There are a few example implementation of this paper in [theano](https://github.com/earcher/nvil_example) and [Matlab](https://github.com/earcher/nvil_example).

---

## 3. Blackbox Variational Inference

##### `Rajesh Ranganath, Sean Gerrish and David M. Blei, 2014`

If I remember well, this is precursor to the NVIL above. Essentially NVIL generalizes this method with an encoder to get variational parameters without needing to resort to the mean-field assumption and therefore uses different variance reduction techniques. The lowerbound for BVI is given by:

$$L(\lambda)=E_{z \sim q_\lambda}[\log p(x, z) - \log q(z \vert \lambda)]$$

Where $$\lambda$$ represents the free parameters. Then the gradients are given as:

$$\nabla L(\lambda)=E_{z \sim q_\lambda}[\nabla_\lambda \log q(z \vert \lambda)(\log p(x, z) - \log q(z \vert \lambda))]$$

and its monte carlo approximation becomes: 

$$\nabla L(\lambda)\approx \frac{1}{S} \sum_{s = 1}^S \nabla_\lambda \log q(z_s \vert \lambda)(\log p(x, z_s) - \log q(z_s \vert \lambda))$$ where $$z \sim q_\lambda(z)$$

This ELBO can be optimized using a gradient based method. But the variance of these gradients estimates is generally to high to work and therefore this method relies on the following variance reduction techniques to reduce this variance:

#### 3.1 Rao-Blackwellization

Suppose we are interested in calculating the expectation of a function, for example the gradients with respect to $$\phi$$ as above. The idea behind Rao-Blackwellization is to replace this function with another function such that the expectation doesn't change but the variance reduces. It does so by using the conditional expectation of the function. 

#### 3.2 Control Variates

This is very similar to the centering and the variance normalization as in the above case of NVIL, so we do not discuss it here.

---

## 4. Generative Adversarial Network (GAN)

I initially wanted to provide a very short description of GANs here although they are generally not explained under the *variational inference*-type framework. But given their popularity I think it is only fair to write a separate post on GANs. If you are interested in the divergence minimization formulation of GANs have a look at the $$f$$-GAN [paper](https://arxiv.org/abs/1606.00709) 

---

## 5. ADVI

Automatic Differentiation Variational Inference generalizes the VAE framework by providing a library of invertible mappings from the distribution (of-interest) domain $$\mathbb{D}^k$$ to $$\mathbb{R}^k$$; which can be used to transform the prior density to build a Gaussian approximation to the posterior. This allows for using the re-parameterization trick for inference using VAE. Since this mappings are invertible the Gaussian approximations can be transformed back to the required domain.

#### 5.1 Implementation

There is a very nice implementation of ADVI in [Stan](http://mc-stan.org/) . A reasonably good implementation is available in [PyMC3](https://pymc-devs.github.io/pymc3/).

---

## 6. Normalizing Flows

Okay I should say that I am quite a fan of this and other related papers on this topic. So I plan on writing atleast a paragraph about each one of them. But that is for later so for now I only have a one-liner: remember how we generally resort to the familliar exponential family in most of the variational inference methods? How our variational posteriors are mostly uni-modal (expect in the case of mixture distributions, but that is a differnet story for another time)? Well, here is a solution to all of that and it's called [Normalizing Flows](http://jmlr.org/proceedings/papers/v37/rezende15.pdf).
