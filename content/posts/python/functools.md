---
title: functools
slug: functools
author: aaron
date: 2023-12-05
tags: ["python", "functools", "decorator"]
categories: ["Python Tips"]
---

`functools` provides a range of features that can greatly simplify your code and make it more efficient. The `functools` module is part of the Python standard library and provides higher-order functions, decorators, and other utilities for working with functions. 

## `functools.partial`: Partial Function Application

Partial function application is a technique where you create a new function by fixing certain arguments of an existing function, allowing you to provide only the remaining arguments when calling the new function. This can be achieved using the `functools.partial` function.

Let's explore an example to understand how `functools.partial` works:

```python
from functools import partial

# A function that calculates the exponential value of a number
def power(base, exponent):
    return base ** exponent

# Create a new function to calculate the square of a number
square = partial(power, exponent=2)

# Call the new function
result = square(5)  # Output: 25
```

In the above example, we defined a function `power` that calculates the exponential value of a number using the `**` operator. By using `functools.partial`, we created a new function `square` which is a specialized version of the `power` function, with the `exponent` argument fixed to 2. Calling `square` with an argument of 5 returned the expected result of 25.

Partial function application is particularly useful when you have a function that requires many arguments but is commonly used with some fixed values. It allows you to create specialized functions that are easier to work with.

## `functools.compose`: Function Composition

Function composition is a technique where you combine multiple functions to create a new function, where the output of one function becomes the input of the next. The `functools` module provides the `compose` function to achieve function composition.

Let's look at an example to illustrate function composition using `functools.compose`:

```python
from functools import compose

# Two functions to compose
def double(x):
    return x * 2

def increment(x):
    return x + 1

# Compose the functions
composed_func = compose(double, increment)

# Call the composed function
result = composed_func(5)  # Output: 12
```

In the above example, we defined two functions, `double` and `increment`, each performing a specific operation on a given number. Using `functools.compose`, we created a new function `composed_func` by composing the two functions together. When we called `composed_func` with an argument of 5, it first applied the `increment` function and then passed the result to the `double` function, resulting in the output of 12.

Function composition allows you to build complex transformations by combining smaller, reusable functions. It promotes code modularity and improves code readability.

## `functools.lru_cache`: Memoization

Memoization is a technique where you cache the results of expensive function calls and reuse them when the same inputs occur again. The `functools.lru_cache` decorator provides a convenient way to implement memoization in Python.

Let's see an example to understand how `functools.lru_cache` works:

```python
from functools import lru_cache

# A recursive function to calculate Fibonacci numbers
@lru_cache(maxsize=None)
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

# Calculate the 10th Fibonacci number
result = fibonacci(10)  # Output: 55
```

In the above example, we defined a recursive function `fibonacci` that calculates the Fibonacci number for a given index `n`. By applying the `@lru_cache` decorator to the function, we enabled memoization. This means that the function's results are cached and reused when the same inputs occur again. The `maxsize=None` argument specifies an unbounded cache size.

Leveraging memoization helps avoid redundant calculations and significantly improves the performance of recursive functions.

## `functools.wraps`: Preserving Function Metadata

The `functools.wraps` decorator is a convenient tool for preserving the metadata (such as function name, docstring, and annotations) of a wrapped function. It helps maintain important information when creating decorators or using higher-order functions. Here's an example:

```python
from functools import wraps

def debug_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        print(f"Calling function: {func.__name__}")
        return func(*args, **kwargs)
    return wrapper

@debug_decorator
def add(a, b):
    """Adds two numbers."""
    return a + b

result = add(2, 3)  # Output: Calling function: add
                    #         5

print(add.__name__)         # Output: add
print(add.__doc__)          # Output: Adds two numbers.
```

In this example, the `debug_decorator` wraps the `add` function and prints a debug message before calling it. By using `@wraps(func)` inside the inner wrapper function, the metadata of the original function is preserved. Without `@wraps`, the wrapper function would have overwritten the metadata of the wrapped function.

## `functools.reduce`: Function Application to Iterable

The `functools.reduce` function allows you to repeatedly apply a function to the items of an iterable, reducing it to a single value. It is similar to the `reduce` function in other programming languages. Here's an example that calculates the product of a list of numbers using `reduce`:

```python
from functools import reduce

numbers = [2, 3, 4, 5]

product = reduce(lambda x, y: x * y, numbers)
print(product)  # Output: 120
```

In this example, we use `reduce` with a lambda function that multiplies two numbers together. The `reduce` function applies this lambda function successively to the items of the `numbers` list, resulting in the final product.

## `functools.cached_property`: Memoized Property

The `functools.cached_property` decorator allows you to create a property that is computed only once and then cached. Subsequent accesses to the property return the cached value, eliminating the need for recalculating it. Here's an example:

```python
from functools import cached_property

class Circle:
    def __init__(self, radius):
        self.radius = radius

    @cached_property
    def area(self):
        print("Calculating area...")
        return 3.14159 * self.radius ** 2

circle = Circle(5)
print(circle.area)  # Output: Calculating area...
                    #         78.53975
print(circle.area)  # Output: 78.53975 (cached)
```

In this example, the `Circle` class has a `radius` attribute and a `cached_property` called `area`. The first access to `circle.area` triggers the calculation of the area, and the value is cached. Subsequent accesses to `circle.area` retrieve the cached value directly, without recomputing it.