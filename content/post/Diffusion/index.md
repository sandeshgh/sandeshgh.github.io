---
title: Diffusion, Flow and Stochastic Interpolants
<!-- stylesheet: style.css  # Path to your CSS file -->
subtitle: 
summary: Diffusion and Flow
authors:
- admin
tags: []
categories: []
date: "2026-02-09"
featured: false
draft: false


# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  caption: 
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []

# Set captions for image gallery.
gallery_item:
- album: gallery
  caption: Default
  image: theme-default.png
- album: gallery
  caption: Ocean
  image: theme-ocean.png
- album: gallery
  caption: Forest
  image: theme-forest.png
- album: gallery
  caption: Dark
  image: theme-dark.png
- album: gallery
  caption: Apogee
  image: theme-apogee.png
- album: gallery
  caption: 1950s
  image: theme-1950s.png
- album: gallery
  caption: Coffee theme with Playfair font
  image: theme-coffee-playfair.png
- album: gallery
  caption: Strawberry
  image: theme-strawberry.png
---
## Summary
The generative modeling landspace has evolved from time-discretized diffusion (DDPM) to the continuous score based models, and recently to Flow Matching and Stochastic Interpolants. They are all connected and they all try to estimate the same instantaneous velocity field to the probability distribution. Once we have clarified the connection, we can use the unifying stochastic interpolant framework to understand and interpret transformations like $x$-space, $v$-space and $\epsilon$-space transformations, and denounce the myths like we estimte noise in diffusion models. 
 

## Diffusion Model

Let's start from the Score Based Generative Model paper [2]. Song et al. demonstrated that DDPM [1] is a time-discretized form of a continuous probability evolution. By using stochastic differential equations (SDEs), we can generalize this evolution to continuous time. We begin with a data distribution, $p_0$ and make it noisy through a Stochastic Differential equation (SDE).

$$ dx = - \frac{\beta}{2} x \ dt + \sqrt{\beta} \ dW \tag{1} $$


where $dW$ is the standard Brownian motion. For simplicity, I am setting $\beta$ as a constant over time, $t$. The beauty here is that the reverse SDE is also analytically tractable:

$$
dx = \Big(- \tfrac{\beta}{2}\ x - \beta\ \nabla_x \log p_t(x)\Big)\ dt + \sqrt{\beta}\ \tilde{dW} \tag{2}
$$

This reverse SDE paves the way to generate data from noise. The forward SDE goes from data distribution to the noise, while the reverse goes from noise to data. So, if we can model the score function($\nabla_x \log p_t(x)$), then we have all the terms to create a model that can generate a data distribution from complete noise. 



### The Probability Flow ODE
A surprising and crucial result is the existence of a reverse ordinary differential equation (ODE) that corresponds to  the same marginal probability densities as the SDE:

$$
dx = \Big(- \tfrac{\beta}{2}\ x - \tfrac{\beta}{2}\ \nabla_x \log p_t(x)\Big)\ dt \tag{3}
$$

Equations (1), (2) and (3) satisfy same Fokker-Planck equation. What that means is that the forward SDE, the backward SDE and the backward ODE, they all share the same marginal distribution $p_t$ for all $t$. When I was new to diffusion model, it was unclear why that is the case. If we compare equations (2) and (3), they differ by $\frac{\beta}{2} \nabla_x \log p_t(x)$ and the stochastic term. The equivalence implies that the stochasticity of the Brownian motion is sort of canceled by the $\frac{\beta}{2}\nabla_x \log p_t(x)$ in the score function. This is actually true and I will talk about this in detail in another blog-post. For now, let's just take that as a fact. So, we have a reverse ODE which looks like:


$$
dx = - \tfrac{\beta}{2}\ (x +s)\ dt  \tag{4}
$$
where $s(x,t) = \nabla_x \log p_t(x)$ is the score function and $v(x,t) =  - \tfrac{\beta}{2}\ (x +s)$ is the velocity field in the reverse direction. To unify these three frameworks, we need to show that we arrive at this exact equation in both flow model formulation and Stochastic interpolants formulation.


## Flow Matching
The idea of flow matching is to find the velocity field that transports a standard Normal distribution to the data distribution. To do this, they first construct the flow map that maps noise $\epsilon$ to a sample $x_t$:

$$
x_t = \psi_t(\epsilon) = a_t x_0 + b_t \epsilon
$$

Then the conditional velocity field at any time $t$ for a sample x is given by the time derivative of the flow map

$$
u_t(x|x_0, \epsilon) = \frac{d}{dt} \psi_t = \dot{b}(t) \epsilon + \dot{a_t}x_0 = \frac{\dot{b}(t)}{b(t)} \big ( x - a_t x_0\big) + \dot{a_t}x_0
$$

The average velocity for the whole distribution at time t is given by taking expectation with respect to the distribution of $x_0$

$$
v(x,t) = E[u_t(x|x_0)] = E[\frac{\dot{b}(t)}{b(t)} \big ( x - a_t x_0\big) + \dot{a_t}x_0] = \frac{\dot{b}(t)}{b(t)} \big ( x - a_t E[x_0|x_t=x]\big) + \dot{a_t}E[x_0|x_t=x] \tag{5}
$$
## Stochastic Interpolants
Another seminal idea is that of stochastic interpolants due to Albergo et al. which establishes a unified analysis method generalizing Diffusion and Flow methods. 

The Stochastic interpolant recipe is as follows:

1. Express $x_t = a(t) x_0 + b(t) \epsilon$
2. Velocity $v(x, t) = \dot{a}(t)\ \mathbb{E}[x_0 \mid x_t = x] + \dot{b}(t)\ \mathbb{E}[\epsilon \mid x_t = x]$
3. The score function $s(x,t) = -b(t)^{-1} \mathbb{E}[\epsilon \mid x_t = x]$


The first thing I want to do here is to show that we obtain exact same velocity field that we obtained before from Flow Matching.
### Stochastic Interpolant is equivalent to Flow Matching
$$
v(x, t) = \dot{a}(t) \mathbb{E}[x_0 \mid x_t = x] + \dot{b}(t) \mathbb{E}[\epsilon \mid x_t = x] \tag{6}
$$

Taking conditional expectation on both sides of:

$$
\mathbb{E}[x_t \mid x_t = x] = a(t)\ \mathbb{E}[x_0 \mid x_t = x] + b(t)\ \mathbb{E}[\epsilon \mid x_t = x] 
$$

$$
x = a(t)\ \mathbb{E}[x_0 \mid x_t = x] + b(t)\ \mathbb{E}[\epsilon \mid x_t = x] \tag{7}
$$
Substituting $\mathbb{E}[\epsilon \mid x_t = x] = \frac{1}{b(t)}(x - a(t)\ \mathbb{E}[x_0 \mid x_t = x])$, we obtain:
$$
v(x,t) = \frac{\dot{b}(t)}{b(t)} \big ( x - a_t E[x_0|x_t=x]\big) + \dot{a_t}E[x_0|x_t=x]
$$

We have shown that the velocity field derived from Flow matching is exactly same as that from the stochastic interpolant. 

### Stochastic Interpolant is equivalent to Diffusion Model
#### Expressing $x_t$ as an interpolant

For a linear SDE of the form 
$
dx = F x\ dt + L\ dW 
$, the solution $x_t$ is Gaussian. Its mean, $m(t)$ and covariance, $P(t)$, evolve via ODE as follows [6]:

$$
m(t) = e^{F(t - t_0)} m(t_0) \tag{8}
$$

$$
P(t) = e^{F(t - t_0)} P(t_0)\ e^{(F(t - t_0))^T} + \int_{t_0}^{t} e^{F(t-u)} L Q L^{T} e^{(F(t-u))^{T}} du \tag{9}
$$

#### Intuition
What these equations mean is suppose you start from a Gaussian distribution with mean and covariance $m(t_0), P(t_))$ respectively, and the system follows above linear SDE. Then at any time, $t$, $x_0$ evolves into a Gaussian distribution with mean and covariances given above.

For our case, since we start from a single sample, $m(t_0) = x_0$ and $P(t_0) = 0$, $F = \frac{-\beta}{2} I$, $L = \sqrt{\beta}\ I$.

Plugging these in, we obtain:

$$
m(t) = x_0 e^{\left(-\frac{\beta t}{2}\right)} 
$$

$$
P(t) = \left(\int_{0}^{t} \beta e^{-\beta (t-u)}\ du\right) I
= \big(1 - \exp(-\beta t)\big)\ I 
$$

Since $x_t$ is Gaussian distrbuted, sample can be written as:

$$
x_t = e^{-\frac{\beta t}{2}} x_0 + \sqrt{1 - e^{-\beta t}}\ \epsilon = a(t). x_0 + b(t). \epsilon \tag{10}
$$



Thus, we have written $x_t$ in an interpolant form where $a(t) = e^{-\beta t / 2}$ and $b(t) = \sqrt{1 - e^{-\beta t}}$.

#### Calculating velocity field
Substituting the score identity 

$$\mathbb{E}[\epsilon \mid x_t = x] = - b(t) s(x,t) \tag{11} $$

into the velocity field   $v(x, t) = \dot{a}(t) \mathbb{E}[x_0 \mid x_t = x] + \dot{b}(t) \mathbb{E}[\epsilon \mid x_t = x] $, we obtain:

$$
v(x, t) = \dot{a}(t) \mathbb{E}[x_0 \mid x_t = x] - \dot{b}(t) b(t) s(x,t) \tag{12}
$$

Now, we compute the time derivative:

Let's introduce a new variable $\tau = e^{-\frac{\beta t}{2}}$. Then,

$$
a(t) = \tau ,   \  b(t) = \sqrt{1 - \tau^2} 
$$


With some algebra, we obtain:

$$
\dot{a}(t) = -\frac{\beta \tau}{2},  \ \dot{b}(t) b(t) = \frac{\beta \tau^2}{2} 
$$

Therefore, the velocity field is given by:

$$
v(x, t) = -\frac{\beta \tau}{2}\Big(\mathbb{E}[x_0 \mid x_t = x] + \tau s\Big) \tag{13}
$$

There is another critical equation that helps us express equivalent relationship. Taking conditional expectation on both sides of interpolant:

$$
\mathbb{E}[x_t \mid x_t = x] = a(t)\ \mathbb{E}[x_0 \mid x_t = x] + b(t) \mathbb{E}[\epsilon \mid x_t = x] 
$$

$$
x = a(t) \mathbb{E}[x_0 \mid x_t = x] + b(t) \mathbb{E}[\epsilon \mid x_t = x] \tag{14}
$$

Substituting

$$
\mathbb{E}[x_0 \mid x_t = x] = \frac{x - b(t) \mathbb{E}[\epsilon \mid x_t = x]}{a(t)} 
$$

into the velocity field, we obtain:

$$
v(x, t) = - \frac{\beta}{2}(x + s) \tag{15}
$$

#### Conclusion: 
Flow Matching, Stochastic Interpolants, and Diffusion models are targeting the same underlying velocity field.


## Myth: We are estimating noise $\epsilon$

One of the most common misconception in diffusion literature is we estimate the noise, $\epsilon$ during training and use that to go from noise to image by subtracting the estimated noise. This gives a sense that we can subtract noise from noisy image to obtain a clean image. This is quite incorrect. 

Yes, we are averaging some noise values, but they are not any random noise values. The meaning of $E[\epsilon | x_t]$ is that we average over only those noise values which lead to the construction of that precise $x_t = x$. So, first, its average noise and second not just any average, but there is special condition on filtering those noise values. Therefore, our estimated $\epsilon$ is very different from the noise.

A more accurate interpretation is we are estimating negative log likelihood and that is very closely related to the velocity vector in which we need to move to reach image from noise. So, the whole point of diffusion modeling is trying to identify the distribution-level velocity vector, such that we can make incremental movements along those directions until we reach the final destination restored images.


## Prediction in $x_0$ space, $\epsilon$ space and $v$ space

In earlier diffusion days, we had papers like DDIM[3] and other who introduced the concept of directly predicting $x_0$ from $x_t$. Somehow, directly predicting $x_0$ and then adding noise to it to bring it back and then again predicting $x_0$ produced better samples. However, it was hard for me to understand what exactly was going on. 

The idea was something like this. Since $x_t = a(t) x_0 + b(t) \epsilon$, we can write 
$$
x_0 = \frac{x_t - b(t) \epsilon}{a(t)}
$$
Now, we would replace the $\epsilon$ with the $\epsilon_{\theta}$ we obtained from training. Using this $x_0$, we would again estimate noisy $x_t$ at a slightly closer time and repeat. If you use auxiliary network to estimate $x_0$, you could generate better samples. Since $\epsilon_{\theta}$ is not noise, it was not clear to me what $\hat{x}_0$ was. 

There was other paper on progressive distillation [4] of diffusion model, which introduced the idea of training in v-space where v represented velocity, defined as the time derivative of $x_t$. In their case, they parameterized $x_t = cos (\phi) x_0 + sin (\phi) \epsilon$. Then they used velocity as $\frac{d}{d \phi} x_t$. Their $\phi$ is a reparameterization of time, $t$, after which their definition of $v$-space coincides with the velocity we have been talking so far. 

The latest paper that talks about $x$ space prediction is Just Image Transformers (JiT)[5]. They use equations like these

$$
x_{\theta} = net_{\theta}
$$
$$
x_t = tx_{\theta} + (1-t) \epsilon_{\theta}
$$
$$
v_{\theta} = x_{\theta} - \epsilon_{\theta}
$$

Without the theory of stochastic interpolants, it is hard to interpret these equations. With stochastic interpolants, we can begin to explain the core ideas behind these space transformations. The key idea that we can take conditional expectation on the interpolant equation $
x_t = a(t)x_0 + b(t)\epsilon$, which gives us

$$
\mathbb{E}[x_t \mid x_t = x] = a(t)\ \mathbb{E}[x_0 \mid x_t = x] + b(t)\ \mathbb{E}[\epsilon \mid x_t = x] 
$$

$$
x = a(t)\ x_{\theta} + b(t)\ \epsilon_{\theta} 
$$
which is true beacuse of the linearity of conditional expectation. In light of this, we can safely say the quantities that the model learns are actually 

$$
x_{\theta} = \mathbb{E}[x_0 | x_t = x] \tag{16}, \
\epsilon_{\theta} = \mathbb{E}[\epsilon \mid x_t = x] 
$$



i.e., expected $\epsilon$ and expected $x_0$. We need to take this together with definition of velocity field for interpolants:

$$v = \dot{a}(t)\ x_{\theta} + \dot{b}(t)\ \epsilon_{\theta}$$

That unifies all the v-space, x-space, $\epsilon$- space modeling from DDIM till JiT.

---

## References
1. Ho, J., Jain, A. and Abbeel, P., 2020. Denoising diffusion probabilistic models. Advances in neural information processing systems, 33, pp.6840-6851.

2. Song, Y., Sohl-Dickstein, J., Kingma, D.P., Kumar, A., Ermon, S. and Poole, B., Score-Based Generative Modeling through Stochastic Differential Equations. In International Conference on Learning Representations.

3. Song, J., Meng, C. and Ermon, S., Denoising Diffusion Implicit Models. In International Conference on Learning Representations.

4. Salimans, T. and Ho, J., Progressive Distillation for Fast Sampling of Diffusion Models. In International Conference on Learning Representations.

5. Li, T. and He, K., 2025. Back to basics: Let denoising generative models denoise. arXiv preprint arXiv:2511.13720.

6. Särkkä, S. and Solin, A. (2019) Applied Stochastic Differential Equations. Cambridge: Cambridge University Press.
