---
title: 100 Days of ML - Day 3
subTitle: Day 3
cover: 100days1.jpeg
category: ml
menuTitle: ml
---

- ## Content for Today

[Linear Algebra Series on YouTube by 3blue1brown](https://www.youtube.com/watch?v=kjBOesZCoqc&index=1&list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab)

## Notes

> - Video 10
---

The cross product of two vectors $\vec{v}$ and $\vec{w}$ is represented as $\vec{v} * \vec{w}$ and there are 2 points to think about the cross product in a geometrical sense

- If we think of the 2 vectors enclosing a parallelogram, then the cross product is the area of that parallelogram.

    $$
    \vec{v}*\vec{w} = det(\begin{bmatrix} a & c \\ b & d \end{bmatrix})
    $$

    Here, 
    
    $$
    \vec{v} = \begin{bmatrix} a  \\ b \end{bmatrix} , \vec{w} = \begin{bmatrix} c  \\ d \end{bmatrix}
    $$

    The $det$ is what gives us the area of the parallelogram.

    Now the parallelogram is constructed by taking copies of $\vec{v}$ and $\vec{w}$ and moving them in 2D space such that the 4 vectors enclose a parallelogram.

- But a cross product in a more sticter gives another vector which 
  - Is perependicular to the paralleogram enclosed by $\vec{v}$ and $\vec{w}$. 
  - The length of which is equal to the area of the parallelogram.
  - The direction of the vector can be calculated by the right hand rule. If the index finger points in the direction of $\vec{v}$ and the middle finger points in the direction of $\vec{w}$ then the thumb gives the direction of the resultant vector.



