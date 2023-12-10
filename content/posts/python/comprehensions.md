---
title: Comprehensions
slug: comprehensions
author: aaron
date: 2023-05-03
tags: ["python", "list comprehension", "dictionary comprehension", "set comprehension", "generator"]
---


In Python, there are several types of comprehensions that can be used to create new data structures from existing ones:

## list comprehension

A list comprehension is a concise way to create a new list by iterating over an existing iterable and applying a transformation or filtering condition to each element. Here's an example:

```python
my_list = [1, 2, 3, 4, 5]
squared_list = [x*x for x in my_list]
print(squared_list)  # Output: [1, 4, 9, 16, 25]
```

In this example, the list comprehension `[x*x for x in my_list]` creates a new list by squaring each element of `my_list`.

## dictionary comprehension

A dictionary comprehension is a concise way to create a new dictionary by iterating over an existing iterable and applying a transformation or filtering condition to each key-value pair. Here's an example:

```python
my_dict = {'a': 1, 'b': 2, 'c': 3}
squared_dict = {k: v*v for k, v in my_dict.items()}
print(squared_dict)  # Output: {'a': 1, 'b': 4, 'c': 9}
```

In this example, the dictionary comprehension `{k: v*v for k, v in my_dict.items()}` creates a new dictionary by squaring each value of `my_dict` and keeping the original keys.

## set comprehension

A set comprehension is a concise way to create a new set by iterating over an existing iterable and applying a filtering condition to each element. Here's an example:

```python
my_list = [1, 1, 2, 2, 3, 3, 4, 4, 5, 5]
my_set = {x for x in my_list if x % 2 == 0}
print(my_set)  # Output: {2, 4}
```

In this example, the set comprehension `{x for x in my_list if x % 2 == 0}` creates a new set by keeping only the even numbers from `my_list`.

## generator comprehension

A generator comprehension is a concise way to create a generator object by iterating over an existing iterable and applying a transformation or filtering condition to each element. Here's an example:

```python
my_list = [1, 2, 3, 4, 5]
squared_generator = (x*x for x in my_list)
for x in squared_generator:
    print(x)
```

In this example, the generator comprehension `(x*x for x in my_list)` creates a generator object that yields the square of each element of `my_list`. The generator is then iterated over using a `for` loop to print each squared value.

Overall, comprehensions in Python providea concise and readable way to create new data structures from existing ones, and they are a powerful feature of the language. In addition to the types of comprehensions mentioned above, there is also a string comprehension which can be used to create a new string by iterating over an existing iterable and applying a transformation or filtering condition to each character. However, this is less commonly used than the other types of comprehensions.

It's worth noting that while comprehensions can be very useful in many cases, they can also become difficult to read and understand if they become too complex. In such cases, it may be better to use a regular loop or a function to achieve the same result.
