# Ramen Bowl Problem
Matthieu Hanania

## Problem Description

There are 100 noodles in your bowl of ramen. You take the ends of two noodles uniformly at random and connect the two, putting the connected noodle back into the bowl and continuing until there are no ends left to connect. On average, how many circles will you create? Round to the nearest whole number.

## Mathematical Explanation

To solve this problem, we use the law of total expectation. We define $ E(n) $ as the expected number of circles formed when starting with $ n $ noodles.

The law of total expectation states that:

 $E(X) = P(A)E(X|A) + P(B)E(X|B) $

In this context:
- Let $A$ be the event where the first pair of ends you pick form a new circle.
- Let $ B $ be the event where the first pair of ends you pick do not form a new circle.

When we connect two ends together, it effectively merge the two noodle into one from the bowl. To form a circle when we have $ n $ noodles, we need to connect the two ends of the same noodle. This means that after selecting one noodle, we are left with $ 2n-1 $ ends, with only one pair of ends that will form a circle.

The probability of forming a new circle is:

 $P(A) = \frac{1}{2n - 1}$ 


Given that the first pair of ends forms a new circle, the expected number of circles in the remaining $ n-1 $ noodles plus one circle is:

$ E(n | A) = E(n-1) + 1 $

Given that the first pair of ends does not form a new circle, the expected number of circles in the remaining $ n-1 $ noodles is:

$ E(n | B) = E(n-1) $

Using the law of total expectation, we get:

$ E(n) = \frac{1}{2n-1} \times (E(n-1) + 1) + \left(1 - \frac{1}{2n-1}\right) \times E(n-1) $

This simplifies to:

$ E(n) = \frac{1}{2n-1} + E(n-1) $



With only one noodle in the bowl, a circle is automatically created, so $E(1)=1$

## Simulation Code

With a simple code simulation, we can get the result

```python
def with_calculted_probabilities(n):
    E=1
    for i in range(2,n+1):
        p = 1/(2*i-1)
        E = p + E
    
    return E
```
> Average number of circles with the calculated probabilities, the for n = 100 noodles: 3


To verify the mathematical solution, we can simulate the process of forming circles by randomly pairing ends of noodles. 

```python
def n_random_noodle(nb_noodles):
    cirles=0

    # Connecting two noodles together results in a single noodle
    while nb_noodles >0:

        ends_1,end_2 = random.sample(range(2*nb_noodles), 2)
        nb_noodles-=1

        # Drawn ends are in the same noodle if their even part is the same (0 and 1, 1 and 2, ...)
        if ends_1//2 == end_2//2:
            cirles+=1
    return cirles    
```
> Average number of circles with the random simulation, for n = 100 noodles: 3
