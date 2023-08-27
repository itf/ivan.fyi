---
title: Winding number in geometric algebra

date: 2021-01-08
updated: 2021-01-08
taxonomies:
    tags: [blog,]
    
extra:
    math: true
    math_auto_render: true
---

From the wikipedia, <https://en.wikipedia.org/wiki/Winding_number#Complex_analysis>, we can see the definition of winding number in complex analysis. 


# 2 dimensions

And so we can adapt it to geometric algebra in 2 dimensions.

Let $\partial M$ be a curve (we are calling it $\delta M$ because we will later perform the analysis using the fundamental theorem of calculus for geometric algebra), and let $j$, be the pseudo scalar in 2 dimensions.

The winding number is:
$$\frac{1}{2\pi j} \oint_{\partial M}  d\mathbf{x} \frac{\mathbf{x}}{|x|^{-2}} = \frac{1}{2\pi j}\oint_{\partial M}  d\mathbf{x} \mathbf{x}^{-1} $$

The scalar component will cancel itself, and just the bivector component is left, therefore we divide by the pseudoscalar. And 2&pi; is the length of the boundary of a circle.

Using the fundamental theorem of calculus for geometric calculus (Alan Macdonald - Vector and Geometric Calculus, section 10.1), supposing that $M$ is a surface. 

$$\frac{1}{2\pi j}\oint_{\partial M}  d\mathbf{x} \mathbf{x}^{-1} = \frac{1}{2\pi j} \int_{ M}  d\mathbf{x^2} \partial\left(\mathbf{x}^{-1}\right)$$

$\partial\left(\mathbf{x}^{-1}\right)$ is equal to 0 at every place except the origin, but we can "include the origin" by using a kronecker delta

$$\frac{1}{2\pi j}\oint_{\partial M}  d\mathbf{x} \mathbf{x}^{-1} = \int_{ M}  d\mathbf{x^2} \delta_\mathbf{x}(\mathbf{x}) = \begin{cases}
    1,& \text{if the volume includes the origin}\\
    0,              & \text{otherwise}
\end{cases}
$$


# More dimensions

We can extend this to more dimensions. Let $n$ be the dimensions, and let $A_n$ be the $n-1$ dimensional area of the $n$ dimensional unit sphere. Then:
$$\frac{1}{A_n}\oint_{\partial M}  d\mathbf{x^{n-1}} \frac{\mathbf{x}}{|x|^n} = \int_{ M}  d\mathbf{x^n} \delta_\mathbf{x}(\mathbf{x}) = \begin{cases}
    1,& \text{if the volume includes the origin}\\
    0,              & \text{otherwise}
\end{cases}
$$

for 3 dimensions you should recognize this equation from the electrical field of a point charge in the origin.


# Using this with functions

Let say you wanna find the $0$s of a function, and you are using the winding number algorithm <https://www.youtube.com/watch?v=b7FxPsqfkOY>. 

TODO

