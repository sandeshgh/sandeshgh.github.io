---
title: A Gentle Introduction to Statistical Learning Theory
subtitle: 
summary: Gentle introduction to Statistical Learning Theory
authors:
- admin
tags: []
categories: []
date: "2019-02-05T00:00:00Z"
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
image:
  caption: ''
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

Suppose you are training a neural network (or using any other method) to solve, say, classification. You choose a certain set as training set, and train your favorite network on it by minimizing loss on that train set. Then, if the loss is within certain threshold, you are happy and you claim that you have a network that works. But, you have probably wondered: What is the guarantee that this model will work in other data points? Why is training on some training set a good idea and ensures that the model will work on test set? Well, intuitively, it makes sense that this is a necessary requirement: if it is a good model, it should at least work on that training set. But, why is it sufficient? You may also convince yourself intuitively that the training set is some finite approximation of the infinite data, where the model should be evaluated; therefore, the model trained infinite approximation is also an approximation. You know intuitively, it sort of makes sense, but, is there a precise way to formalize these intuitions and talk in a much more quantitative way? The advantage of a precise, mathematical argument (over a qualitative) is that it can answer the question of following type: what can I say about the rate at which error decreases if I keep increasing data from the distribution? 

These questions must have bothered, at some point, everyone who has been working with machine learning. It also bothered early researchers in this field, as a result of which principled ways were proposed to try to answer these questions; these principled approaches are collectively studied and referred to as Learning Theory. Statistical Learning Theory is usually used to refer to works that focus on the statistical perspective while answering these questions, and usually refer to the line of work first pioneered by Vladmir Vapnik and later explored by many others. 

This blog is, obviously, scratching the surface of Statistical Learning Theory. But, my focus here is on intuition backed by mathematical reasoning. Many a times, I see intuitions and interpretations floating around without quantitative backing, which makes the arguments quite imprecise. On the other end of the extreme, dry mathematical derivation without adequate intuition and explanations might seem esoteric and boring to many. Many a times, it prevents readers from appreciating the beauty of reason, which, ironically, is actually the point of Mathematics.

This blog is a downsampled picture: it gives overview, provide global context but misses details at many places. After reading this, I believe the readers will have clear big picture, and can fill in the details wherever deemed necessary. Before beginning, I would like to acknowledge that the contents of this blog is based on and inspired from tutorial due to Bousquet et al.[1] and notes of Percy Liang[2] and has used references from there.
## Problem Definition
Let us consider a supervised learning problem, where $\mathcal{X}, \mathcal{Y}$ denote input domain and target domain respectively. For simplicity, assume there exists a probability measure $P(x,y)$ on the product space $\mathcal{X} \times \mathcal{Y}$. Let $\mathcal{D}_n = \{ (x_1,y_1), (x_2, y_2), ...,(x_n,y_n) \} $ be a randomly sampled set of $n$ data points from the distribution $P(x,y)$. Then we term

$
R_n=\frac{1}{n} \sum_i\left[ \ell(f(x_i),y_i)\right]$

$
R= E_{x,y \sim P(x,y)}\left[ \ell(f(x),y)\right]
$
, where $R_n$ is called the empirical risk and $R$ is called the expected risk. Usually, we do not have access to the true distribution $P(x,y)$ and therefore, we only use the finite sample $\mathcal{D}_n$ to estimate an optimal function $f_n$, i.e.,

$$
f_n= \underset{f}{argmax} \hspace{0.2cm} R_n
$$
Since, $f_n$ is not optimized based on true distribution, but rather on an empirical set $\mathcal{D}_n$, it is not the true optimial function, say ${f^\*}$ . The objective of statistical learning theory is to try and quantify how worse this $f_n$ is in comparison to the true $f^*$.



To introduce basic statistical learning theory, it is important to have a good intuition about the ideas upon which the theory is based on: the concentration inequalities. So, bear with me while I start from some concentration inequalities. It might actually be beneficial if we forget about the statistical learning theory for the moment.

# Concentration Inequalities
## Markov Inequality

<img src="/img/Markov.jpg" alt="x is greater than a"
  width="600" />

Let's define a function
    \begin{equation}
    f(x)=\boldsymbol{1}_ {X\geq a} =
    \begin{cases}
      1 & \text{if}\ X \geq a \\ ; 
      \hspace{0.2cm} 0 & \text{otherwise}
    \end{cases}
    \end{equation}
Then,
$$
a \boldsymbol{1}_ {X\geq a} \leq X
$$
Taking expectation with respect to X,
$$
a \textbf{E}[\boldsymbol{1}_ {X\geq a}] \leq \textbf{E} [X]
$$

$$
a [0.P(X < a)+1.P(X\geq a)] \leq \textbf{E} [X]
$$
$$
a [P(X\geq a)] \leq \textbf{E} [X]
$$

$$
P(X\geq a) \leq \frac{\textbf{E} [X]}{a}
$$


## Chebyshev Inequality
Setting $X=Y-\mu$ where $\mu = \textbf{E} [Y]$
$$
P(|Y-\mu|\geq a) \leq \frac{\textbf{E} [|Y-\mu|]}{a}
$$

$$
P(|Y-\mu|^2\geq a^2) \leq \frac{\textbf{E} [|Y-\mu|^2]}{a^2}
$$

$$
P(|Y-\mu|^2\geq a^2) \leq \frac{Var(Y)}{a^2}
$$

These inequalities tell us that it is possible to bound the error. It is interesting that when we think about probability distributions, we think of them as source of randomness. But, here we saw that statistics also provide us guarentees that things are not arbitrarily random. More precisely there is a way in which we can quantify how random things are. THis forms the basis of the statistical learning theory. In one line, the idea of statistical learning theory is to use these guarentees to say, okay things cannot go worse than this.

## Q. What is the intuition behind these inequalities?
These inequalities tell us about the certainty implicit in a random variable. For example, the Chebyshev inequality tells us that the probability that a random variable deviates away from its mean by a quantity that is proportional to the variance of the random variable and inversely proportional to the level probability value. This is quite intuitive since if a random varible has high variance, it is likely to deviate away from its mean. But, perhaps, what is surprising is that this inequality gives us an upper bound on how far a random variable can deviate from its mean. Of course, this is in probability, meaning that there is always some chance that this event might happen. 



## Q. How is this relevant to learning theory?
In learning theory, we want to use these guarantees in bounding the probabiliyt of error. 

# From Concentration Inequality to Generalization Bounds
## Change of Variables
Let $z=(x,y)$ and let us define a function $g$ such that we have,

$$
R_n(g)=\frac{1}{n} \sum_i\left[ \ell(f(x_i),y_i)\right] = \frac{1}{n} \sum_i g(z_i)$$

$$
R(g)= E_ {z \sim P(z)} \left[ \ell(f(x),y) \right] = E_{z \sim P(z)} g(z)
$$

Then, empirical risk minimization and expected risk minimization can be written as

$$
g_n= \underset{g \in \mathcal{G}}{argmax} R_n(g)
$$

$$
g^\*= \underset{g \in \mathcal{G}}{argmax} R(g)
$$

### Generalization Gap
$$
\Delta =  E_ {z \sim P(z)} g_ n(z) - {E_ {z \sim P(z)} g^\*(z)} = R(g_n) - R(g^\*)
$$

The interpretation of this equation is as follows. Suppose, we had somehow access to the true distribution $P(z)$. Then, we would have obtained a true minimizer $g^\*$ by minimizing the expected risk. But, now, due to lack of access to true distribution, we can only have an empirical risk minimizer, i.e. $g_n$. Now, to access how good this empirical risk minimizer is, we again try to compute the difference of true risk by plugging in two minimizer. The difference in the performance between our empirical risk minimizer and true expected risk minimizer is termed as the generalization gap.

## Using concentration inequality in the derivation of bound
For the moment, let's fix the function $g=g_ 0$ and pay attention to the difference $R_ n (g_ 0) - R(g_ 0)=\frac{1}{n} \sum_ i g_ 0(z_ i) - E_ {z \sim P(z)} g_ 0(z)$. First, note that $R_ n (g_ 0)$ is a random variable and the whole source of randomness comes from the fact that $n$ samples are randomly drawn from the distribution $P(z)$. Also, note that this argument is valid because $g_ 0 $ is fixed and does not depend on the data $\mathcal{D}_ n$. Second, note that in this case $R(g_ 0)$ is the mean of the  random variable $R_ n (g_ 0)$ because of the law of large numbers. This implies that we could immediately apply concentration inequality to make statements like the following: 
$$
P(|R_ n(g_ 0) - R(g_ 0)| \geq \epsilon) \leq \frac{V}{\epsilon}
$$ 

## Finitely many  and Union Bound

In the above analysis, we assumed that the function $g$ is fixed. Therefore, we could apply concentration inequality because all the stochasticity came from the data points selected.
To bound the generalization gap, we need to bound the quantity like ... ,but where the function g is not fixed, but rather is something like $g_ n$, i.e. Empirical risk minimizer. Now, if we plug in this function $g_ n$ in above inequality, we cannot use concentration inequality because $g_ n$ is a function of data points in a very complicated way and therefore, the argument of mean of random variables is no longer valid: there will be dependence on different $g_ n$ depending on the correlation of data points and true $g^ *$ is also not guarenteed to be mean of those.

To avoid this difficulty, we take a very inefficient approach. We consider all the function in some function space $\mathcal{G}$. We fix each of those functions and write the concentration inequality for each of them. This must be true because we do this without the knowledge of data. Then, we compute the probability of union of the events that each of the function is within some $\epsilon$ such that the union of all those is less than $1-\delta$.
This is known as the union bound. 

Eq...


Notice that we added the probability of error of each function. This is necessary because ...


In the end, we see that the error probabilty is directly proportional to the number of functions (cardinality of a finite set) in the function space. 

## How is this related to Generalization Gap
For the moment, assume that function space from which ERM is taken is a finite function space as considered above. Then, note the following:
.....
.. is always greater than 0 since...
We see that generalization gap is twice of the bound we just derived. 

## Intuitions and takeaways
Until now, we derived for a function space with finitely many functions. In the next section, we will show that the result can be generalized to infinitely many functions with more sophisticated mathematics, but the intuition holds: generalization bound will become propotional to the size of function space instead of number of functions in function space. 
In other words, the number of functions is replaced by some "measure of complexity" in infinite case as follows:

..Eq..


Following is the summary and take away so far:

Concentration inequalities give us bound on how a random variable can deviate from its mean. 

If we fix a function, and use iid assumption this can be used to derive a bound

If function space has many functions, the bound is proportional to the number of functions (or size of function space)

Generalizatio gap is twice of the above bound, so we are done.



It is noteworthy that we derived bound in a very crude way. We make argument in a statistical sense and derive a pessimistic bound, i.e. in the worst case the probability of error cannot go beyond this. Because of these reasons, it is expected that this bound might be quite loose and that may hinder its usefulness. At the end of this blog, we will talk about how this concern has manifested and taken a serious form in the context of deep learning.



# How to deal with infinitely many functions ?

## A Roadmap 


## VC Dimension

# Criticism 

## Criticism of Union Bound



