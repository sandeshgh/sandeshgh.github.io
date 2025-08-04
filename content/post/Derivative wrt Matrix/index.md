---
title: Derivative with respect to Matrix
<!-- stylesheet: style.css  # Path to your CSS file -->
subtitle: 
summary: Derivative wrt Matrices
authors:
- admin
tags: []
categories: []
date: "2024-08-04"
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
# Preface
"What does it actually mean to take derivative of a loss function with respect to a matrix ?" I was wondering some day during my PhD. 

"A matrix is nothing but a bunch of numbers structured in a 2D format. So, you just take derivative of loss with respect to each of these numbers and then put them in the same format at the corresponding position. That's what the derivative of a loss with respect to that matrix is".

Okay, that is very convenient, but at the same time quite tedious thing to do if we have to do it by hand. 

"I'm sure there should be some smart way to go about this. What is that?"

This blog is what I discovered as an early PhD student and today I decided I share that with others who might be wondering too.


# Differentiating with respect to Vector
Before going into matrix derivative, let's think about derivative vector. Let $y=f(x)$ be a scalar valued function of a vector $x$; i.e., $f:\mathbb{R}^{m}\rightarrow \mathbb{R}$. Think of this as a loss function depending on some vector of dimension $m$.

The derivative $\frac{dy}{dx}$ is a vector $\big [ \frac{dy}{dx_j} \big]$. By convention, we assume all vectors are column vectors and transpose whenever we need row vectors.
Also, $[a_j]$ denotes a vector with individual elements $a_j$.

## Example:
Let $x=
\begin{bmatrix} 
x_1 \\\\ 
x_2 
\end{bmatrix}$
and $y=x_1^2+3x_2^4$.
Then, $\frac{dy}{dx}=\begin{bmatrix} 2x_1 \\\\ 12x_2^3 \end{bmatrix}$.

Note that the column vector $\big [ \frac{dy}{dx_j} \big]$ is constructed by putting the derivative of $y$ with respect to the $j^{th}$ element of $x$ at the $j^{th}$ position.

We are interested in developing tools where we can perform such derivation directly. For example, if $A$ is any matrix and $y=x^TAx$, then we want to be able to show $\frac{dy}{dx}=(A+A^T)x$. This can be shown with cumbersome calculation as follows:

Let $A=\begin{pmatrix} a_{11} & a_{12} 
\\\\
a_{21} & a_{22} \end{pmatrix}$.
Then, $y=\begin{bmatrix} x_1 & x_2 \end{bmatrix} \begin{bmatrix} a_{11} & a_{12} \\\\ a_{21} & a_{22} \end{bmatrix} \begin{bmatrix} x_1 \\\\ x_2 \end{bmatrix}$
$=a_{11}x_1^2+a_{21}x_1x_2+a_{12}x_1x_2+a_{22}x_2^2$.

$\frac{dy}{dx}=\begin{bmatrix} 2a_{11}x_1+(a_{21}+a_{12})x_2 \\\\ (a_{21}+a_{12})x_1+2a_{22}x_2 \end{bmatrix}=(A+A^T)x$.

However, we want to do this in an easier way. Moreover, we also want the technique to be useful for deriving derivative with respect to matrices.

## Use of Differentials

Using Taylor expansion:
$f(x+dx)=f(x)+(\frac{df}{dx})^{T}dx+$ higher terms

The key idea here is that if we take $dx$ sufficiently small, then $dy=f(x+dx)-f(x)=(\frac{df}{dx})^{T}dx$. Why? Because all the rest of the terms are higher powers of $dx$ and will converge to zero in the limiting case. In fact, the very definition of derivative comes from this limiting case of Taylor expansion if we think about it. So, we can use this trick to compute derivative. Hence, given any function $f(x)$, we calculate $dy=D^Tdx$ and then obtain $\frac{dy}{dx}=D$.

## Example:
$y=f(x)=x^TAx$

$dy=(x+dx)^TA(x+dx)-x^TAx$$=x^TAx + x^TAdx + dx^TAx + dx^TAdx - x^TAx$

In the limiting case, as $dx \to 0$:

$dy=x^TAdx + dx^TAx$

Using $dx^TAx = x^TA^Tdx$ (because $dx^TAx$ is a scalar, so it's equal to its transpose),

$dy=x^TAdx + x^TA^Tdx = x^T(A+A^T)dx$.
Therefore, $\frac{dy}{dx}=(A+A^T)x$.

Using the same procedure, it is easy to show $\frac{d}{dx}(w^Tx)=w$.

This technique of using differentials is powerful because we can use the same technique to find derivative with respect to matrices.

# Derivative with respect to matrices

Let $f$ be a function of matrices. We denote $y=f(X)$, where $X=[x_{ij}]$.
Note that $y$ is scalar.
What does it mean by derivative w.r.t. matrix? $f:\mathbb{R}^{m \times n}\rightarrow \mathbb{R}$.
The derivative $\nabla_{X}y = \begin{bmatrix} \frac{\partial y}{\partial x_{ij}} \end{bmatrix}$.
That is, we differentiate $y$ with respect to each element of matrix $X$, $\frac{\partial y}{\partial x_{ij}}$, and then we fill the $(i,j)^{th}$ position of the matrix with this derivative to obtain the required derivative.

Interestingly, we can use the same procedure of differentials to find derivative with respect to matrices.

### Steps to calculate derivative w.r.t. matrix X:
1.  $dy=f(X+dX)-f(X)$
2.  Express $dy=tr(D^T dX)$
3.  $\nabla_Xy=D$

Why is there a trace of $D$ and $dx$? Because at this point we need to define the inner product of two matrices. The Taylor series equivalent with matrix as argument requires us to define inner product in the matrix space. For now we can think of that $tr(D^T dX)$ is inner product of two matrices $D$ and $dX$. To see this you can take two matrices of $2\times2$ and see that this expression gives us a scalar and satisfies inner product properties like linearity and norm etc.
## Example 1:
$\frac{d}{dX} tr(XBX^T) = X(B+B^T)$

**Proof:**

$dy = tr[(X+dX)B(X+dX)^T] - tr(XBX^T)$

Setting higher terms of $dX$ to zero:

$dy = tr(dXBX^T + XBdX^T)$

Using property $tr(AB) = tr(BA)$ and $tr(A+B) = tr(A)+tr(B)$:

$dy = tr(dXBX^T) + tr(XBdX^T)$

$dy = tr(BX^T dX) + tr(B^T X^T dX)$

$dy = tr[(B+B^T)X^T dX]$

Therefore, $\frac{dy}{dX}=X(B+B^T)$.

## Example 3:
$\frac{d}{dX}[tr(AX^{-1})]=-(X^{-1}AX^{-1})^{T}$

**Proof:**
By now you must have realized from above exercise that the differential operator is linear. So, we can apply some tricks like moving differential operator inside another linear operator like trace. A direct application of something like this is as follows:

$d[tr(AX^{-1})]=tr(AdX^{-1})$.

At this point, we use the following identity: $dX^{-1}=-X^{-1}dX X^{-1}$ ---(1)

The proof will be provided later. For now using this identity:

$dy=tr(A(-X^{-1}dX X^{-1}))$

$=tr(-AX^{-1}dX X^{-1})$

Using the cyclic property of trace, 
$tr(ABC)=tr(BCA)=tr(CAB)$:

$=tr(-X^{-1}AX^{-1}dX)$.

Therefore, $\frac{dy}{dX}=-(X^{-1}AX^{-1})^T$.

**Proof of equation (1):**

$d(I)=0$.

Or, $d(XX^{-1})=0$.

Or, $X dX^{-1} + dX X^{-1}=0$.

$dX^{-1}=-X^{-1}dX X^{-1}$.

## Example 4:

$\frac{d}{dX}\ln|X|=(X^{-1})^T$.

Proof of example 4 includes the identity $d\ln|X|=tr(X^{-1}dX)$ --- (2).

For proof of this identity, see the Convex Optimization book [2].

Using (2):

$\frac{d}{dX}\ln|X| = (X^{-1})^T$.

## References

1. Caltech EE150 Lecture 5 Slides](http://www.systems.caltech.edu/dsp/ee150_acospc/lectures/EE_150_Lecture_5_Slides.pdf)
2. https://web.stanford.edu/~boyd/cvxbook/bv_cvxbook.pdf
