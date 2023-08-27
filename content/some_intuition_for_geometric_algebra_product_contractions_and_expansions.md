---
title: Some intuition for Geometric Algebra product contractions and expansions

date: 2020-11-15
updated: 2020-11-15
taxonomies:
    tags: [math,]
extra:
    math: true
    math_auto_render: true
---
One of the best materials for learning about inner product contractions is, [The Inner Products of Geometric Algebra](https://www.researchgate.net/publication/2842332_The_Inner_Products_of_Geometric_Algebra), by Leo Dorst.
Here I'll write some intuition to help you remember those results.

First, notice that every product is linear, therefore we can always think about what happens in a product by thinking about what happens with the orthogonal and parallel components. We will use the term "dimension", in a very informal way. For example, if I have the vector $e_1$ and the vector $e_2$, and we "sum" their dimensions, we obtain $e_1 \wedge e_2$. If we have the blade $e_1 \wedge e_2$ and we remove the dimension $e^1$, we obtain $e^2$. 


# $$a \cdot (B \wedge C)$$

Lets start with:
$$a \cdot (B \wedge C)$$ , where $B$ and $C$ are $k$-blades with $k\ge1$. What this formula is saying, intuitively, is that we take 2 blades, $B$ and $C$, we add their dimensions, to get a blade of higher dimension, and then we remove the dimensions of $a$.

For the product to not be null. at most one of $B$ or $C$ has the dimension of $a$. If it is $B$, then the formula is equivalent to 
$$(a \cdot B) \wedge C)$$
Because removing the dimension of $a$ from $B \wedge C$, is equivalent to removing it from $B$, and then adding the dimension $C$.

If instead it is $C$, then, we need to remove the dimension of $a$ from $C$, so we will have a term $$\pm? B \wedge (a \cdot C)$$, where we need to reason about what should the sign be. 

We can split $C$ into 2 parts, $a \wedge C'$, therefore we have 
$$a \cdot(B \wedge a \wedge C') = a \cdot(a \wedge \hat{B} \wedge C') $$,
where $\hat{B}$ is the grade inversion of B, i.e. equal to $-B$, if $B$ is odd. Therefore, 

$$a \cdot (B \wedge C) = (a \cdot B) \wedge C) + \hat{B} \wedge (a \cdot C)$$  

In other words, when taking the dot product of a vector with a blade, we can just "put" the vector next to the terms it would cancel, while taking into account grade inversion. For exmple:

$$e_1 \cdot(e_2 \wedge e^1 \wedge e^3) = - e_2 \wedge (e_1 \cdot e^1 \wedge e^3) = -e_2 \wedge e_3$$


# Contraction

The inner product/ dot product are slightly ambiguous. If we have $(A \cdot B)$, we don't know if we are removing dimensions from $B$ or from $A$, i.e. supposing that $A$ is an $a$-blade and $B$ is a  $b$-blade, we don't know if  $(A \cdot B)$ is an $a-b$-blade or $b-a$-blade, since we don't know which of them has the higher dimensions. So we define the left contraction inner product $A \lrcorner B$  to be removing the dimensions of $A$ from $B$, i.e. an $a-b$-blade (or 0, if $b>a$.

With this, we can think about:
$$(A \wedge B) \lrcorner C =(A \lrcorner (B \lrcorner C))  $$
i.e. removing the dimensions of both $A$ and $B$ from $C$ is the same as removing the dimensions of $B$ from $C$, and then removing the dimensions of $A$ from the result.

