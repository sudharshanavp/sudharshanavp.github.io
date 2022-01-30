---
layout: post
title: 'Solving Project Euler: Problem 1'
date: 2022-01-30 13:39 +0530
math: true
categories: [Project Euler]
tags: [Programming, Math, Python, Project Euler]
---
## Why Project Euler?

I've always liked Math and Programming as a kid, there's a satisfying feeling I get when I successfully solve a problem and that's one of the reasons I choose to study engineering. Even though I like Math and Programming I've never been really that good at it so I thought that Project Euler would help me hone my skills in both Math and Programming. The computational problems of Project Euler vary in difficulty but they're very interesting with many having different ways to solve it.

I thought I'd document my journey through solving these problems so here we are! There are a few things to note before we begin:

* I use HackerRank as my platform to solve these problems, HackerRank has the first 250 problems of Project Euler as a challenge on their website. I like the HackerRank platform so I'll be using this.
* The programming language that I'll be using is Python because that's the language I'm currently focusing on.

## Problem 1: Multiples of 3 and 5

HackerRank Link: <https://www.hackerrank.com/contests/projecteuler/challenges/euler001/problem>

If we list all the natural numbers below 10 that are multiples of 3 or 5, we get 3, 5, 6 and 9. The sum of these multiples is 23.
Find the sum of all the multiples of 3 or 5 below N.

### My Solution

#### Brute Force Approach

This is a fairly simple problem at first glance. You can brute force your way through it by iterating through all the numbers till N and check whether it's a multiple of 3 or 5.

The code for that would be like this:

```python
import sys
t = int(input().strip())
for a0 in range(t):
    n = int(input().strip())
    sum = 0
    for i in range(n):
        if i % 3 == 0 or i % 5 == 0:
            sum+=i
    print(sum)
```

Now this will work for small values of N like a 1000 or 10000, but for the constraints of the problem in HackerRank where N can $10^9$ this approach is too slow. The time complexity of the brute force method is $O(n)$ which is not too slow but there's another Mathematical approach with a time complexity of $O(1)$ which is basically instantaneous.

#### Mathematical Approach

Our main aim here is to find the sum of all multiples of $3$ or $5$ between $1$ and $N$. To approach this problem we can use the concept of Triangular Numbers. You can read about Triangular Numbers [here](https://byjus.com/maths/triangular-numbers/), but what we need is the formula for the sum of N Natural Numbers and that is 

$$ T_{n} = \sum_{k=1}^{N}k=1+2+3+…+N=\frac{N(N+1)}{2} $$

With this we can proceed further. Let's first consider multiples of 3, the sum of multiples of $3$ is

$$ 3+6+9+12+15+...+n_3 $$

where $n_3 = 3*(N/3)$

If we take $3$ as common from the equation than we get

$$ 3*(1+2+3+4+5+..+(N/3)) $$

using the formula for the sum of $N$ natural numbers, the above equation can be simplified as

$$ 3* \frac{N/3(N/3+1)}{2} $$

When we do the same thing for multiples of $5$ we get

$$ 5*\frac{N/5(N/5+1)}{2} $$

so the equation for sum of multiples of $3$ or $5$ should be the sum of the above two equations that is

$$3*\frac{N/3(N/3+1)}{2} + 5*\frac{N/5(N/5+1)}{2}$$

but using this equation wouldn't give you the right answer.

You see, multiples of 3 and multiples of 5 have common multiples. They are $15, 30, 45, 60, 90 ...$, there's a pattern here and it is that all the common multiples of $3$ and $5$ are multiples of $15$. These multiples get added up twice, once in the sum of all multiples of $3$ equation and once in the sum of all multiples of $5$ equation. So we need to subtract it from  the equation, hence we find the sum of all multiples of $15$ and subtract this sum from the above equation. Therefore our final equation would be

$$3*\frac{N/3(N/3+1)}{2} + 5*\frac{N/5(N/5+1)}{2} - 15*\frac{N/15(N/15+1)}{2} $$

Coding this is simple, for the division in python you need to be a bit careful and use integer division `(// operator)` as the normal division returns a float and we don't need decimal numbers here.

```python
def sum(n , k):
    d = n // k
    return (k * d * (d+1)) // 2

import sys
t = int(input().strip())
for a0 in range(t):
    n = int(input().strip())
    print(sum(n - 1,3) + sum(n - 1, 5) - sum(n - 1,15))
```

This is the final code, works like a charm and is in constant time $O(1)$ instead of linear time $O(n)$. This can handle cases of astronomically large numbers like $10^{30}$. 
