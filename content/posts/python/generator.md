---
title: Generator
slug: generator
author: aaron
date: 2023-04-07
tags: ["python", "generator", "fibonacci"]
categories: ["Python Tips"]
---

In Python, a generator is a special type of function that can be used to create iterable sequences of values on-the-fly. Unlike regular functions, which compute and return a value immediately, generators can generate a sequence of values over time, using the yield keyword.

Example: The following `fib` function is a generator function that generates a sequence of Fibonacci numbers up to a given limit index `n`.

```python
def fib(n):
    a = [0, 1]
    i = 0
    while i <= n:
        yield a[i%2]
        a[i%2] = a[0] + a[1]
        i += 1
```

The `yield` keyword is used to return each generated Fibonacci number as it is generated, which makes the function a generator.

Use `next` to get each number:

```shell
>>> f=fib(5)
>>> next(f)
0
>>> next(f)
1
>>> next(f)
1
>>> next(f)
2
>>> next(f)
3
>>> next(f)
5
>>> next(f)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```
