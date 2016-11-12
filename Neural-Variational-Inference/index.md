---
layout: default
title: "Blackbox and Approximate Neural Inference"
---
# Blackbox and Approximate (Variational) Neural Inference 
For quite sometime now I've been working on neural inference methods that have become very popular recently. There is an abundance of resources on these methods and that is precisely why I decided to write a considerably terse post about the most prominent of such techniques. Since this is only an attempt to summarize the vast body of work being done in this field, I will try to provide links to more detailed (read: much better than mine) posts and paper for each of the methods. As mentioned earlier, this is only an attempt to summarize this fairly sofesticated field, please correct me via comments if you find any mistakes in my description, of which I can promise there will be plenty to fix :) Lastly before starting, this is more of a *dynamic* post, meaning that I will kepp updating the entries and adding details as I get time.

With that lets delve staright into our main topic, __Approximate Neural Inference__ or as we will refer to it throughout this text, __NI__. Simply put, varitional inference (__VI__) is a deterministic method of carrying out approximate inference in probabilistic models when the posterior distribution over the variables of interest (or the latent state) is intractable. In order to do so, VI uses a tractable family of distributions to approximate the intractable posterior in an optimization procedure that usually minimizes the negative log-likelihood of the data that the model is trying to fit. Consider the following example,

### Example

Let $$p_\Theta(x)=\int_zp(x\vert z,\alpha)p(z\vert \beta)dz$$ be the likelihood of our data $$x$$ under our model parametrized by $$\Theta=\{\alpha,\beta\}$$ where $$z$$ (continuous or discrete in which case $$\int$$ can be replaced by $$\sum$$) is a latent variable. Assuming, the posterior distribution $$p_\theta(z\vert x)$$ is intractable, mean-field VI (which is a type of VI) approximates this posterior by first introducing variational parameters $$\phi$$ for each $$z$$ and then aprroximate the true posterior $$p_\theta(z\vert x)$$ by the variational posterior $$q_\phi(z\vert x)$$. In practice, instead of directly optimizing the negative log-likelihood to fit the posterior, VI methods use a simpler to optimize lowerbound on it (popularly referred to as the __ELBO__ or the evidence lowerbound). Traditional VI methods make use of *conjugate* priors over the latent variables to derive closed form `EM-like` updates for optimization, which accounts for their fast speed of inference. But this is also the reason for their limited applicability and/or accuracy. Not all models can leverage the convinience of conjugate priors. Another drawback is the need of repeated derivations for even minor changes in initial assumptions. __NI__ can be thought of as an alternative form or approximate varitational inference that has a certain *black-box* characteristic to it and therefore allows for carrying out approximate inference without the need to derive update equations even in the models that do not have conjugate priors. 

I think that is all that we need to know from traditianal VI theory to proceed further. The only other thing that needs to be spelled out is the actual __ELBO__ that is optimized in the old methods can be written down in two equivallent ways as follows,

$$\log p_\Theta(x)\geq
\log p_\Theta(x)-D_{KL}[q_\phi(z\vert x)\vert \vert p_\theta(z\vert x)]=
E_{z \sim q}[\log p_\alpha(x\vert z)]-D_{KL}[q_\phi(z\vert x)\vert \vert p_\gamma(z)]$$.

---

## 1. Variational Autoencoder (VAE) 

##### `Kingma and Welling, 2013`

VAE uses the following ELBO, $$E_{z \sim q}[\log p_\alpha(x\vert z)]-D_{KL}[q_\phi(z\vert x)\vert \vert p_\gamma(z)]$$. Where within the KL term instead of using the posterior $$p_\theta(z\vert x)$$ it regularizes the variational posterior by the prior $$p_\gamma(z)$$ over $$z$$.The benefit of this change is that unlike the (intractable) posteriors, priors are always available in Bayesian methods. The problematic term is the expectation over the log conditional of the data $$\log p_\alpha(x\vert z)$$. While this expectation cannot always be computed, it can always be approximated using *Monte-Carlo* (__MC__) given we can sample from the variational posterior. Considering that is true for at least some exponential family distributions we can therefore estimate the EBLO.

VAEs use a feed-forward neural network, called the *inference network* for generating the parameters $$\phi$$ of the variational posterior and a *recognition network* for decoding the data. Using an inference network for generating variational distribution imposes a certain smoothness assumtion over the data-points and hence instead of having a mean-filed type local parameters, the network allows sharing of global variational parameter. Training this network is problematic because by using MC for approximating the expectation in the above ELBO, discontinuity is introduced in the graph and hence back propogation is not possible. Back propogating through random sampler is a well studied problem and the way VAE solve it is by using the __reparametrization trick__/__Mat-trick__ which is applicable to any continuos distribution that has a __non-centered parametric form__. I do not want to get in detail of these tricks here as that would require a lot more space than I have, so I will finish this description of VAEs by saying that VAEs can be used as a __neural inference__ method for a large class of continuos latent state model where the prior over the latent variable has a __non-centered parametric form__. Recently, we also showed that VAEs can be used for __Dirichlet__ priors like in a topic model using __Laplace Approximation__. Details can be found [here](http://openreview.net/forum?id=BybtVK9lg). In future I will update this section for the more recent stuff such as,

#### 1.1 Normalizing Flows and Beyond

#### 1.2 Component Collaping in VAEs and Trianing Tricks

#### 1.3 Using VAEs to Infer LDA-type Topic Models

---

## 2. Neural Variational Inference Learning 

##### `Mnih and Gregor, 2014`

NVIL is a more general method of inference that is equally applicable to both continuous and discrete latent state probabilistic models. Lets start by considering how the ELBO is transcribed as an expectation in NVIL by absorbing the prior over $$z$$ into the joint of the model,

$$L(x,\Theta,\phi)=E_{z \sim q}[\log p_\Theta(x, z) - \log q_\phi(z\vert x)]$$

Like VAEs, in NVIL the variational posterior $$q_\phi(z\vert x)$$ is constructed using an inference network as well. The gradients of this ELBO *w.r.t* to $$\Theta$$ and $$\phi$$ are given as follows,

$$\nabla_\Theta L(x) = E_{z \sim q}[\nabla \log p_\Theta(x, z)]$$ and 

$$\nabla_\phi L(x) = E_{z\sim q}[(\log p_\Theta(x, z) - \log q_\phi(z\vert x))* \nabla_\phi \log q_\phi(z\vert x)]$$.

There is no problem with approximating $$\nabla_\Theta L(x)$$ with MC but the high variance in the MC approximation of $$\nabla_\phi L(x)$$ requires additional methods to train succesfully. To this end, the authors proposed two black-box methods of variance reduction in the gradient estimates. 

#### 2.1 Centering the Learning Signal

A one line description (I will expand this later) of this technique: The expectation in the learning signal remains invariant if a constant $$c$$ is substracted from it. Therefore, a systematically calcualted constant quantity $$C(x)$$ when substracted from the learning signal can help bring the noise down in the gradients. 

#### 2.2 Variance Normalization

For the time being, I would only say that it is similar to carrying out __batch-normalization__. As above, I will expand this subsection over time.

Although it is designed to be a black-box method, NVIL also allows benefiting from the local structure of the model.

---

`...to be continued...`

## 3. Blackbox Variational Inference

## 4. Generative Adverserial Network (GAN)

## 5. ADVI
