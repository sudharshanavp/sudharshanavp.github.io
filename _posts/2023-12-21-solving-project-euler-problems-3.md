---
layout: post
title: 'Solving Project Euler: Problem 3'
categories:
- Project Euler
tags:
- Python
- Math
- Programming
- Project Euler
math: true
date: 2023-12-21 17:00 +0530
---
## Even Fibonacci Numbers

Project Euler Prompt

The prime factors of $13195$ are $5, 7, 13$ and $29$.

What is the largest prime factor of the number $600851475143$?

## Solution

### First Approach

The code is fairly straightforward, I wrote a general method to find out the largest prime

```python
import math

def largest_prime(n):
    prime_factors = 0

    while n % 2 == 0:
        prime_factors = 2
        n /= 2
    
    # n is odd at this point
    for i in range(3, int(math.sqrt(n)+ 1), 2):
        while n % i == 0:
            if i > prime_factors:
                prime_factors = i
            n /= i
    
    if n > prime_factors:
        prime_factors = n

    print(prime_factors)
```

#### How does this code work 

There are three main steps we are using here

1. Step 1 is to take care of numbers that are even, we repeatedly divide the number by 2 until the number becomes odd.
2. Step 2 is to take care of the odd numbers, we start the range from 3 and increment the numbers by 2 here because 2 is the only even prime factor.
    1. Now, the reason why we have used $\sqrt n + 1$ here is because of a simple property of composite numbers that every composite number has a prime factor either lesser or equal to it's square root.
    2. So what we do is find the least prime factor, remove all occurences of it by dividing the number by the least prime factor and repeat it until the number reduces to either $1$ or a prime number
3. whenever we encounter a prime number we check if it's larger than the existing prime number and if it is we replace it.