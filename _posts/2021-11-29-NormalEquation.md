---
title: 'Normal Equation'
date: 2021-11-29
excerpt: "Derivation of the Normal Equation for linear regression"
permalink: /2021-11-29-NormalEquation/
tags:
  - Machine Learning
---

Introduction
======
The Normal Equation provides an analytical solution for linear regression with a least-squares cost function. This solution is advantageous 
in comparison to the solution provided by a numerical algorithm (like gradient descent) because no iteration is required and no learning rate
\\((\alpha)\\) needs specified. Many derivations of this powerful equation exist online, but I wanted to share my own notes on its derivation 
because it explains how one can use the properties of the <i>trace</i>.

Trace of a Matrix
======
The <i>trace</i> of square matrix \\(A\\) is defined by the summation over \\(A\\)'s diagonal entries

$$tr(A) = \sum\limits_{i}A_{ii}$$

Note that since the <i>trace</i> is defined only for the diagonal elements, transposing the matrix has no effect on the resultant trace, i.e.,

$$tr(A) = tr(A^T)$$

If we have another compatible matrix \\(B\\), it can be verified that 

$$tr(AB) = \sum\limits_{i}\Big[AB\Big]_{ii} = \sum\limits_{i}\sum\limits_{j}A_{ij}B_{ji}$$ 

Similarly, if we have another compatible matrix \\(C\\), it is likewise verified that 

$$tr(ABC) = \sum\limits_{i}\Big[ABC\Big]_{ii} = \sum\limits_{i}\sum\limits_{j}\sum\limits_{k}A_{ij}B_{jk}C_{ki}$$

The <i>trace</i> operation is a linear mapping, meaning that it satisfies the additivity and homogeneity properties:

$$tr(A + B) = tr(A) + tr(B)\\$$

$$tr(\alpha A) = \alpha tr(A)$$

The final relevant property for our derivation of the Normal Equation is the cyclic property: if the matrix product of 
ABC yields a square matrix, then

$$tr(ABC) = tr(BCA) = tr(CAB)$$

Derivative of the Trace of a Matrix
======
Based upon \\((4)\\), we now can write that for a row \\(j\\) and a column \\(k\\)

$$
\begin{align}
\frac{\partial tr(ABC)}{\partial B_{jk}} &= \sum\limits_{i}A_{ij}C_{ki}\\
&= \Big[CA\Big]_{kj} \\
&= A^TC^T
\end{align}$$

Similarly, if matrix \\(B\\) were written with its transpose, \\(B^T\\), then

$$
\begin{align}
\frac{\partial tr(AB^TC)}{\partial B_{kj}} &= \sum\limits_{i}A_{ij}C_{ki}\\
&= \Big[CA\Big]_{kj} \\
&= CA && \text{[1]}
\end{align}$$

Normal Equation for Linear Regression: Least-Squares Cost Function
======
We are now equipped with the tools to derive the Normal Equation. Following from the development of [2], we define our 
design matrix as \\(X\\), our weights (coefficients) as \\(\theta\\), and our labeled data/target values as \\(y\\). Utilizng a 
least-squares cost function, we write the cost over all \\(m\\) training examples as a vector-vector inner product

$$
\begin{align}
J(\theta) &= \frac{1}{2m}(X\theta - y)^T(X\theta - y)\\
&= \frac{1}{2m} (y^T - \theta^TX^T)(X\theta - y)\\
&= \frac{1}{2m} \Big(y^TX\theta + \theta^TX^Ty - y^Ty - \theta^TX^TX\theta \Big)
\end{align}
$$

Since the least-squares cost function is convex, our cost function has only one optima. Therefore, we can find the optimal weights for our
linear regression model simply by computing the gradient of our cost function with respect to our weights. Before continuing, it is worth mentioning
a final property of the <i>trace</i>. If \\(A\\) is a 1-by-1 matrix, then its <i>trace</i> is simply a real number, i.e., the only element
in the matrix. Thus

$$
\begin{align}
J(\theta) &= \frac{1}{2m} \Big(y^TX\theta + \theta^TX^Ty - y^Ty - \theta^TX^TX\theta \Big)\\
&= \frac{1}{2m} tr\Bigg(\Big(y^TX\theta + \theta^TX^Ty - y^Ty - \theta^TX^TX\theta \Big)\Bigg)
\end{align}
$$

Now, computing the gradient of our cost function: 
$$
\begin{align}
\nabla_\theta J(\theta) &= \nabla_\theta \frac{1}{2m} tr\Bigg(\Big(y^TX\theta + \theta^TX^Ty - y^Ty - \theta^TX^TX\theta \Big)\Bigg)\\
&= \frac{1}{2m} \nabla_\theta \Bigg(tr(y^TX\theta) + tr(\theta^TX^Ty) - tr(y^Ty) - tr(\theta^TX^TX\theta)\Bigg) && \text{Linearity}\\
&= \frac{1}{2m}\nabla_\theta \Bigg( tr(X\theta y^T) + tr(y\theta^TX^T) - tr(y^Ty) - tr(X\theta\theta^TX^T) \Bigg) && \text{Cyclic property}\\
&= \frac{1}{2m} \Bigg( X^Ty + X^Ty - 0 - \Big( X^TX\theta + X^TX\theta\Big) \Bigg) && \text{Derivative rules}\\
&= \frac{1}{2m} \Bigg( 2X^Ty - 2X^TX\theta \Bigg)\\
&= \frac{1}{m} \Bigg( X^Ty - X^TX\theta\Bigg)
\end{align}
$$

All that remains is finding the extrema by setting the gradient to \\(0\\)

$$
\begin{align}
\nabla_\theta J(\theta) = 0 = \frac{1}{m} \Bigg( X^Ty - X^TX\theta\Bigg)\\
\end{align}
$$

$$X^TX\theta = X^Ty \\$$

$$\theta = (X^TX)^{-1}X^Ty$$

which yields the Normal Equation as desired.

References
======
[1] Traa, J. Matrix Calculus - Notes on the Derivative of a Trace. http://paulklein.ca/newsite/teaching/matrix%20calculus.pdf.

[2] Ng, A. (2000). CS229 Lecture notes. CS229 Lecture notes, 1(1), 1-3.

------