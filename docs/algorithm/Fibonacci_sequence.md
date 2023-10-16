---
layout: default
title: Fibonacci Sequence
parent: Algorithm
nav_order: 2
paginate: 5
---

## Fibonacci Sequence

### Problem:

Fibonacci Sequence is sequence which each number is the sum of it's preceding numbers. 

    0,1,1,2,3,5,8,13,21,34,55,


### Solution:

    In order to calculate fib(n), only need to know f(n-1) and f(n-2). 

        fib(n) = fib(n-1) + fib(n-2)

    As an recurssive solution, it must have break condition.

```python

    def fib(n):
        if n == 0 or n == 1 return n
        return f(n-1) + f(n-2)

    fib(10)

```
