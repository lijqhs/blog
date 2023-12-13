---
title: Array
slug: array
author: aaron
date: 2023-04-01
tags: ["python", "numpy"]
categories: ["Python Tips"]
# ShowBreadCrumbs: false
# draft: true
---

In Python, an array is a data structure that stores a collection of elements of the same data type. Unlike lists, which can contain elements of different data types, arrays can only contain elements of a single data type, such as integers, floats, or characters.

Python supports two types of arrays: arrays provided by the built-in `array` module and arrays provided by the `numpy` module.

## built-in `array` module

The `array` module provides a simple way to create and manipulate arrays of primitive data types, such as integers, floats, and characters. Here's an example of using the `array` module to create an array of integers:

```python
import array

my_array = array.array('i', [1, 2, 3, 4, 5])
print(my_array)
```

In this example, the `array` function is used to create a new array of integers with the values `[1, 2, 3, 4, 5]`.

The first argument to the `array` function is a type code that specifies the data type of the array. In this case, the type code `'i'` represents signed integers.

|TYPECODE|C TYPE|PYTHON TYPE|SIZE|
|--|--|--|--|
|'b'|signed char|int|1|
|'B'|unsigned char|int|1|
|'u'|wchar_t|Unicode character|2|
|'h'|signed short|int|2|
|'H'|unsigned short|int|2|
|'i'|signed int|int|2|
|'I'|unsigned int|int|2|
|'l'|signed long|int|4|
|'L'|unsigned long|int|4|
|'q'|signed long long|int|8|
|'Q'|unsigned long long|int|8|
|'f'|float|float|4|
|'d'|double|float|8|

see [more](https://docs.python.org/3/library/array.html)

## `numpy` module

The `numpy` module provides a more powerful and flexible way to create and manipulate arrays, including support for multi-dimensional arrays, mathematical operations on arrays, and advanced indexing and slicing. Here's an example of using the `numpy` module to create an array of integers:

```python
import numpy as np

my_array = np.array([1, 2, 3, 4, 5])
print(my_array)
```

In this example, the `np.array` function is used to create a new array of integers with the values `[1, 2, 3, 4, 5]`.

The `numpy` module also provides many other functions and tools for working with arrays, such as `ndarray.shape` and `ndarray.reshape` for manipulating the shape of arrays, `ndarray.min`, `ndarray.max`, and `ndarray.mean` for computing statistics on arrays, and `ndarray.dot` and `ndarray.transpose` for performing matrix operations on arrays.

Overall, arrays are a useful data structure in Python for storing and manipulating collections of elements of the same data type, and they can be used in a wide range of applications, such as numerical computing, data analysis, and machine learning.
