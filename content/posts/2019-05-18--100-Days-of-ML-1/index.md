---
title: 100 Days of ML - Day 1
subTitle: Day 1
cover: 100days1.jpeg
category: ml
menuTitle: ml
---

- ## Content for Today

[Linear Algebra Series on YouTube by 3blue1brown](https://www.youtube.com/watch?v=kjBOesZCoqc&index=1&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

![Linear Algebra Image](https://i.imgur.com/WbUFXRv.png)

## Notes


> - #### Video 1
---

Basic introduction about linear algebra.

> - #### Video 2
---

Generally, we assume $\vec{i}$ as the standard along x axis and $\vec{j}$ as the standard along y axis. Let $\vec{i} + \vec{j}$ represent a vector in the 2D plane. Think of this vector as a single point in the 2D space as $(1,1)$. We can then represent it as a matrix also.

$$
\begin{bmatrix} \vec{i} + \vec{j} \end{bmatrix} =  \begin{bmatrix} 1 \\ 1 \end{bmatrix} \begin{bmatrix} \vec{i} & \vec{j} \end{bmatrix}
$$

This kind of shows the thought process of thinking matrices in a geometrical sense.


**Span** of 2 vectors $\vec{u}$ and $\vec{v}$ is basically the set of vectors that can be generated by scaling these two vectors and then combining them linearly. Taking two scalars $a$ and $b$ the span can be written as $a \vec{u}+b \vec{v}$.

There are 3 cases now - 

- $\vec{u}$ and $\vec{v}$ are not in the same direction. Then the span of these 2 vectors will be the set of all the vectors that exist in the 2D space because you can scale the vectors by any scale with $a$ and $b$ and then combine them linearly.
- $\vec{u}$ and $\vec{v}$ align in the same direction then the span of the 2 vectors will be limited to a line.
- 2 vectors are $\vec{0}$ then you will be stuck on a single point.

Two vectors are linearly dependent if one can be represented as linear transformation of other

$$
\vec{u} = a\vec{v}
$$

Here $\vec{u}$ is linearly dependent on $\vec{v}$


> - #### Video 3 - Linear Transformation
---

Transformation can be thought of as moving around in space. You take an input vector and tranform it into some output vector. But since every type of transformation can be complicated, we only limit ourselves to linear transformations here.

Now to move around you have to make sure these 2 conditions hold

1. Grid lines are always straight and evenly spaced. 
2. The origin always remain fixed.

Now let's assume we initially had a vector $\vec{v}$ as a linear combination of $\vec{i}$ and $\vec{j}$ where $\vec{i}$ and $\vec{j}$ are scaled using x and y.

$$ 

\vec{v} = x\vec{i} + y\vec{j} 

$$

Once we transform the vector in space all we need to know is the new position of $\vec{i}$ and $\vec{j}$. The new $\vec{v}$ will the linear combination of these tranformed $\vec{i}$ and transformed $\vec{j}$ scaled by x and y.

$$

\vec{v} = x\hspace{0.1cm}Tranformed\hspace{0.1cm}\vec{i} + y\hspace{0.1cm}Tranformed\hspace{0.1cm}\vec{j}

$$

Let's assume coordinates of $\vec{v}$ are $(x,y)$ and can be represented as $\begin{bmatrix} x \\ y \end{bmatrix}$ in a $1*2$ matrix. Similarly, let the new position of $\vec{i}$ be $(a,b)$ or $\begin{bmatrix} a \\ b \end{bmatrix}$ and new position of $\vec{j}$ be $(c,d)$ or $\begin{bmatrix} c \\ d \end{bmatrix}$.

Now we can write the new position of $\vec{v} = \vec{v'}$ as 

$$

\vec{v'} = x\vec{i'} + y\vec{j'}

$$

$$

\vec{v'} = x\begin{bmatrix} a \\ b \end{bmatrix} + y\begin{bmatrix} c \\ d \end{bmatrix} \tag{1}

$$ 

$$

\begin{bmatrix} x' \\ y' \end{bmatrix} = x\begin{bmatrix} a \\ b \end{bmatrix} + y\begin{bmatrix} c \\ d \end{bmatrix}

$$

$$

\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} xa \\ yb \end{bmatrix} + \begin{bmatrix} xc \\ yd \end{bmatrix}

$$

$$

\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} xa + yc \\ xb + yd \end{bmatrix}

$$

Finally,

$$

x' = xa+yc

$$

$$

y' = xb+yd

$$

We can reduce equation 1 as 

$$
\begin{bmatrix} x' \\ y' \end{bmatrix} = \begin{bmatrix} a & c \\ b & d  \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}

$$

So $\begin{bmatrix} a & c \\ b & d  \end{bmatrix}$ is essentially what we need to tranform a vector. The first column $\begin{bmatrix} a \\ b \end{bmatrix}$ represents the transformed $\vec{i}$ and second column $\begin{bmatrix} c \\ d \end{bmatrix}$ represents the transformed $\vec{j}$.

Multiplication of $\begin{bmatrix} a & c \\ b & d  \end{bmatrix}$ with a matrix of size $1 * 2$ computationally means linearly transforming the vector in 2D space. 

If you want to discuss anything, hit me up on Twitter at this [thread](https://twitter.com/harshk2301/status/1129808664737398784?s=20).