---
title: Simple proof weak master theorem

date: 2018-09-12
updated: 2020-07-26
taxonomies:
    tags: [blog,]
    
extra:
    math: true
    math_auto_render: true
---

For a 006 student piazza question. Te student liked my answer so I decided to share!


# Work per level:

Suppose you have:

$$T(n) = a T(n/b) + n^c$$

The amount of work done on the root of the tree is:

$$n^c$$.

The amount of work done in the next level is:

$$n^c \frac{a}{b^c}$$

so on the $i^{th}$  level, considering the root to be level 0, is:

$$n^c \left(\frac{a}{b^c}\right)^i$$


# Number of levels

Given that the size of an element of the tree decreases by $b$ in each level, e.g. $n$ -> n/b, n/b^2&#x2026;

An element of the tree will have size 1 at the level:
$$\log_bn$$


# Total work on the tree

The total amount of work on the tree is therefore:

$$\sum_{i=0}^{\log_bn} n^c \left(\frac{a}{b^c}\right)^i = n^c \sum_{i=0}^{\log_bn} \left(\frac{a}{b^c}\right)^i $$

This naturally leads to 3 cases:

$$ \left(\frac{a}{b^c}\right) >1$$

$$ \left(\frac{a}{b^c}\right) = 1$$

$$ \left(\frac{a}{b^c}\right) < 1$$


# Case 1: $$\frac{a}{b^c}<1$$

You have a geometric series of ratio < 1:

$$n^c \sum_{i=0}^{\log_bn} \left(\frac{a}{b^c}\right)^i \le n^c$$

$$ \sum_{i=0}^{\infty} \left(\frac{a}{b^c}\right)^i = n^c \frac{1}{1-\left(\frac{a}{b^c}\right)}$$

And this new term is just a constant

So:

$$\theta ( n^{c})$$


# Case 2: $$\frac{a}{b^c}=1$$

Now the amount of work per level is the same, so:

$$n^c \sum_{i=0}^{\log_bn} \left(\frac{a}{b^c}\right)^i= n^c \sum_{i=0}^{\log_bn} 1 = n^c \log_bn $$


# Case 3: $$\frac{a}{b^c}>1$$

The easiest way to deal with this case is to simply turn the tree upside down.

The amount of work done at the leaves of the tree is the same as the number of leaves on the tree, which is:

$$a^{\log_b n} = \left(b^{\log_ba} \right)^{\log_bn} = \left(b^{\log_bn} \right)^{\log_ba} = n^{\log_ba}$$

At every level above the leaves, the amound of work is multiplied by

$$\frac{1}{\frac{a}{b^c}} = \frac{b^c}{a}$$

So the total amount of work done in the tree is:

$$ \sum_{i=0}^{\log_bn} n^{\log_ba} \left(\frac{b^c}{a}\right)^i = n^{\log_ba} \sum_{i=0}^{\log_bn} \left(\frac{b^c}{a}\right)^i $$

$$\le n^{\log_ba} \sum_{i=0}^{\infty} \left(\frac{b^c}{a}\right)^i = n^{\log_ba} \frac{1}{1-\left(\frac{b^c}{a}\right)}$$

And similar to the first case, this is simply

$$\theta ( n^{\log_ba})$$

