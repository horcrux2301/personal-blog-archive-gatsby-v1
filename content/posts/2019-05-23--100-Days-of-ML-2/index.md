---
title: 100 Days of ML - Day 2
subTitle: Day 2
cover: 100days1.jpeg
category: ml
menuTitle: ml
---

- ## Content for Today

[Linear Algebra Series on YouTube by 3blue1brown](https://www.youtube.com/watch?v=kjBOesZCoqc&index=1&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

## Notes

> - Video 4
---

We have already covered that if we see a matrix multiplication like one below

$$
\begin{bmatrix} a & c \\ b & d \end{bmatrix} \begin{bmatrix} x \\ y \end{bmatrix}
$$

This essentially means

$$

x\begin{bmatrix} a  \\ b  \end{bmatrix} + y \begin{bmatrix} c \\ d \end{bmatrix}

$$

So this sum of scaled versions of columns of the matrix is essentially matrix multiplication. (Linearly scaling $x$ by the place where $\vec{i}$ lands (1st column of the matrix is where $\vec{i}$ lands) and linearly scaling $y$ by the place where $\vec{j}$ lands (2nd column of the matrix is where $\vec{j}$ lands)).

Matrix multiplication of two $2*2$ matrices

<!-- Given two matrices $\begin{bmatrix} a & c \\ b & d \end{bmatrix}$ and $\begin{bmatrix} e & g \\ f & h \end{bmatrix}$ and their multiplication. -->

Let's assume we are given the following - 

$$

\begin{bmatrix} a & c \\ b & d \end{bmatrix} * \begin{bmatrix} e & g \\ f & h \end{bmatrix}

$$

Then we can understand it as linear transformation of a vector by second matrix and then linear transformation of the resultant vector by the first matrix.

Notice how we first use the second matrix and then the first matrix. This is because doing the other way will give us a different linear transformation, proving that matrix multiplication is not commutative.

# Properties of matrix multiplication


1. **Commutative** ❌ - Matrix multiplication is not commutative. A important property to satisfy while multiplying 2 matrices is that if the dimensions of first matrix are $a*b$ and second matrix are $c*d$ then $b=c$ should hold. If we change the order then this property can no longer hold.
2. **Associativity** ✅ - Matrix multiplication is associative. $A(BC) = (AB)C$. Notice how we don't change the order of multiplication. This point had me confused, because if matrix multiplication is not commutative then why is it associative? We keep the order of multiplication same. <!-- 3. To imagine this we can think of it as first applying result of linear transformation of $A*B$ and then transform the resultant with $C$. Which is same as -->
3. **Distributive** ✅ - Matrix multiplication is distributive. $A*(B+C) = A*B + B*C$

> - Video 5
---

**Linear transformation in 3D** can be thought of as a matrix of 9 numbers (a $3*3$ matrix).

$$
\begin{bmatrix} a & d & g \\ b & e & h \\ c & f & i  \end{bmatrix}
$$

The first column represents the place where $\vec{i}$ lands after the linear transformation is done. Similarly second and third column represent where $\vec{j}$ and $\vec{k}$ land respectively.

> - Video 6
---

**Determinant** of a matrix can be thought of the area by the factor of which the area of a unit side square (in 2D) and the volume of a unit side cube (in 3D) changes after applying the linear transformation. So essentially how much the space is expanded away or squished together.

For eg if the matrix is $\begin{bmatrix} 2 & 0 \\ 0 & 3 \end{bmatrix}$ then it can be thought of scaling $\vec{i}$ 2 times in the $x$ direction and scaling $\vec{j}$ 3 times in the $y$ direction. The area of the unit square will change by $6$ units which is the determinant of the matrix.

Negative determinant gives the indication that the orientation of the space has been flipped.For 2D orientation it can be thought of as if $\vec{i}$ is in the right of $\vec{j}$ then the determinant will be positive. Otherwise the determinant will be negative. For 3D if we use our right hand and point index finger in $\vec{i}$ and middle finger in $\vec{j}$ and thumb points to $\vec{k}$ then the determinant will be positive. If we have to use our left hand then we can assume that the orientation is flipped and the determinant will be negative.

> - Video 7
---

If we have a system of linear equations in 3 variables

$$
2*x+5*y+3*z=-3
$$

$$
4*x+8*y+0*z=0
$$

$$
1*x+3*y+0*z=2
$$

Then we can represent them as matrices

$$
\begin{bmatrix} 2 & 5 & 3 \\ 4 & 8 & 0 \\ 1 & 3 & 0 \end{bmatrix}\begin{bmatrix} x \\ y \\ z \end{bmatrix} = \begin{bmatrix} -3 \\ 0 \\ 2\end{bmatrix}
$$

$$
A \vec{x} = \vec{v}
$$

So we need to find a $\vec{x}$ which when linearly transformed by $A$ in the 3D space lands on $\vec{v}$ .

Now in order to solve this we can think of this in the reverse way. We can try to transform $\vec{v}$ in the 3D space which when transformed lands on $\vec{x}$. The matrix which represents this reverse transformation on $\vec{v}$ is called the inverse of the matrix.

$$
\vec{x} = A^{-1}\vec{v}
$$

For eg if $A = \begin{bmatrix} 0 & 1 \\ -1 & 0 \end{bmatrix}$ represents $90\deg$ clockwise rotation then it's inverse will be 90 deg anticlockwise rotation using matrix $A^{-1} = \begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}$

Also let's calculate $AA^{-1}$

$$
\begin{bmatrix} 0 & 1 \\ -1 & 0 \end{bmatrix} * \begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}
$$

The resultant matrix we get $\begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$ is called the **identity matrix** and applying transformation on any vector using this matrix will cause no change in the original vector. So $AA^{-1}$ is same as first transforming the vector by $A$ and then transforming by the inverse of $A$ i.e $A^{-1}$ which is same as doing nothing.


Now there are 2 cases to consider here - 

1. $det(A) \neq 0$. <!--which means that after the transformation the space increases and the lines move away.--> In such case we can find a way to reverse the transformation and go back to $\vec{x}$ from $\vec{v}$ and a solution exists. So in order to solve our equations all we have to do is multiply both sides by $A^{-1}$.

$$
A^{-1}A\vec{x} = A^{-1}\vec{v}
$$

$$
I\vec{x} = A^{-1}\vec{v}
$$

$$
\vec{x} = A^{-1}\vec{v}
$$

2. $det(A) = 0$. In this case the lines are squished. So in a 2D plane all the vectors can be squished to a line or a point. There is no way here to reverse the transformation. You cannot convert a line to vectors in multiple dimensions.

**Rank of a matrix**

Rank of a matrix tells us number of dimensions in the output matrix after applying the transformation.

So if the output of a transformation is a line the rank is said to be 1. If the output is a plane the rank is 2 and similarly if the output is all of 3D space the rank is said to be 3.

Set of all possible outputs of a linear transformation is called **column space**. In other words, it is the number of dimensions in the output matrix after applying the linear transformation.

When the rank is as high as it can be, i.e it is equal to number of columns then we call the matrix **Full Rank**.

In 2D if we apply a linear transformation on a matrix that isn't full rank such that the final result is a line, then there is a whole line of vectors which land on the origin.

In 3D if we apply a linear transformation on a matrix that isn't 
full rank such that the final result is a plane, then there is a whole line of vectors which land on the origin.

In 3D if we apply a linear transformation on a matrix that isn't full rank such that the final result is a line, then there is a whole plane of vectors which land on the origin. 

<!-- This set of vectors is called the Null Space or the Kernel of the matrix. -->

> - Video 8
---

If we consider non square matrices then we should think about how we can visualise them in a geometrical sense.

Let's assume we have a $3*2$ matrix $\begin{bmatrix} 2 & 3 \\ -1 & 2 \\ 5 & 8 \end{bmatrix}$. Then we can imagine this as a vector in 2D space being transformed into a 3D space. The first column $\begin{bmatrix} 2 \\ -1 \\ 5 \end{bmatrix}$ represents the $\vec{i}$ being transformed to the point $(2,-1,5)$ and the second column $\begin{bmatrix} 3 \\ 2 \\ 8 \end{bmatrix}$ represents the $\vec{j}$ being transformed to the point $(3,2,8)$. 

Similarly if we have a $2*3$ matrix $\begin{bmatrix} 2 & 3 & 4 \\ -1 & 2 & 1 \end{bmatrix}$, then we can imagine this as a vector in 3D space being transformed into a 2D space. We can say this because the matrix has 3 columns which means we start with a vector in 3D space. The matrix has 2 rows which means that the landing positions of the vectors can be represented by only 2 coordinates, meaning that the final vector is in 2D space. The first column $\begin{bmatrix} 2 \\ -1\end{bmatrix}$ represents the $\vec{i}$ being transformed to the point $(2,-1)$, the second column $\begin{bmatrix} 3 \\ 2 \end{bmatrix}$ represents the $\vec{j}$ being transformed to the point $(3,2)$ and the third column $\begin{bmatrix} 4 \\ 1 \end{bmatrix}$ represents the $\vec{k}$ being transformed to the point $(4,1)$ and all 3 are in a 2D space.

Now imagine if we want to transform a vector from 2D space into 1D space. Our matrix will have 2 columns since we start from 2D space and only one row since in 1D space only 1 coordinate will tell us the landing points of our original vectors from 2D space. So $\begin{bmatrix} 2 & -1\end{bmatrix}$ is one such valid matrix which transforms a vector from 2D space into 1D space. The $\vec{i}$ lands at $(2)$ on the line and $\vec{j}$ lands at $(-1)$ on the line.

<!-- > - Video 9
--- -->

Discussion thread for this blog on Twitter - [Link](https://twitter.com/harshk2301/status/1132572043805773825?s=20)



