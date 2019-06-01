---
title: 100 Days of ML - Day 4
subTitle: Day 4
cover: 100days1.jpeg
category: ml
menuTitle: ml
---

- ## Content for Today

[edX Course on Probability]() - Unit 1 - Probability Models and Axioms

## Notes

1. **Probability** is the mathematical way of dealing with uncertainity. So if we are given an experiment we try to find out with what certainty an outcome is going to occur.
2. **Sample Space ($\Omega$)** - A sample space is the set of all possible outcomes in an experiment. For eg - If we toss a coin our sample space will be $({H,T})$. 
    
    A sample space should satisfy following two properities
    - **Mutually exclusive** - After the experiment we should be able to pick one and only one value from the set of sample space to correctly signify our outcome. In other words for one single experiment we should not need more than 1 value from the sample space to signify our outcome.
    - **Collectively exhaustive** - For any experiment that we conduct, the outcome should always be in the set of our sample space.
3. **Finite Sample Space** - An experiment like rolling a die with four faces has finite sample space. We have 4 possible results for each roll and if we roll the die twice there are 16 possible outcomes.
4. **Continuous Sample Space** - Throwing a dart in a square of side 1 has continuous or infinite sample space. We don't know where the dart will lie on the square. The sample space can be defined as

    $$
    \Omega = \{(x,y) | 0 \leq (x,y) \leq 1\}
    $$

    So basically a collection of points $(x,y)$ on the 2D space will define our sample space where $x$ and $y$ are real numbers. We have infinite real numbers so our sample space will be infinite.
5. **Event** is the subset of sample space. And probability is assigned to events.
6. **Axioms** 
    - **Non negativity** - Let's assume we have an event $A$ then $P(A) \geq 0$ will always hold. Probabilities are numnbers between 0 and 1.
    - **Normalization** -If $\Omega$ signifies the entire sample space then $P(\Omega)=1$. This is because no matter the outcome, it will be always an element of sample space.
    - **Additivity** -If $A \cap B = \phi$ then $P(A \cup B) = P(A) + P(B)$. This can be thought of entire sample space as butter spread on a bread. If we consider 2 different spreads of butter on this bread with no common intersection point then the combined spread will be the individual spreads combined.
7. Let's assume we have an event $A$ then the rest of the events in the sample space $\Omega$ can be denoted by $A^c$. 
    $$
    P(\omega) = 1 \\
    \Rightarrow P(\omega) = P(A \cup A^c) = 1\\
    \Rightarrow P(\omega) = P(A) + P(A^c) = 1\\
    \Rightarrow P(A) + P(A^c) = 1 \\
    \Rightarrow P(A) = 1 - P(A^c)
    $$

    So the probability of an event $A$ will always be $\leq1$ because probability of $A^c$ will be $\geq0$.

8. Let's assume we have 3 events $A,B$ and $C$. Also these 3 events are non-intersecting events meaning $A \cap B \cap C = 0$.

    Now, 

    $$
    P(A \cup B \cup C) = P((A \cup B) \cup C) \\ 
    \hspace{73pt} = P(A \cup B) + P (C) \\ 
    \hspace{85pt} = P(A) + P(B) + P(C)
    $$

    This argument can be extended for any number of disjoint sets. 
    
    $$
    P(A_{1} \cup A_{2} \cup \ldots A_{n}) = P(A_{1}) + P(A_{2}) + \ldots + P(A_{n})
    $$

9. Some more axioms

    If $A\subset B$ then $P(A)\leq P(B)$

    Proof - 

    $$
    B = A \cup (B \cap A^c) \\ 
    \Rightarrow P(B) = P(A \cup (B \cap A^c)) \\
    \Rightarrow P(B) = P(A) + P(B \cap A^c) \\
    $$

    Now $P(B \cap A^c) \geq 0$ which means we add something to $P(A)$ to make it equal to $P(B)$, which means that $P(B) \geq P(A)$.

    $P(A \cup B) = P(A) + P(B) - P(A \cap B)$

    Proof - 

    

