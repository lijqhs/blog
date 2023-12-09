---
title: Arguments in Python
slug: arguments-in-python
author: aaron
date: 2023-05-02
tags: ["python", "keyword arguments", "positional arguments"]
---

In Python, there are several ways to pass arguments to a function, including positional arguments, keyword arguments, default arguments, variable-length argument lists (`*args`), and variable-length keyword argument dictionaries (`**kwargs`). The choice of argument passing method depends on the specific requirements of the function and the nature of the data being passed.

Here's a brief overview of the different argument passing methods in Python:

- **Positional arguments**: Positional arguments are passed to a function based on their position in the argument list. Positional arguments are the most common type of function argument in Python and are used to pass arguments to a function in a specific order. Positional arguments are matched to function parameters based on their position in the argument list.

- **Keyword arguments**: Keyword arguments are passed to a function based on their name, rather than their position in the argument list. Keyword arguments are useful when you want to specify arguments by name, or when you want to pass optional arguments to a function. Keyword arguments are matched to function parameters based on their name.

- **Default arguments**: Default arguments are used to specify default values for function parameters. Default arguments are used when a parameter is not passed a value during the function call. If a parameter is not passed a value during the function call, the default value is used instead.

- **Variable-length argument lists (`*args`)**: Variable-length argument lists, also known as "unpacking argument lists," are used to pass a variable number of arguments to a function. The `*args` parameter is used to collect all the positional arguments passed to the function into a tuple, which can then be looped over and processed inside the function.

- **Variable-length keyword argument dictionaries (`**kwargs`)**: Variable-length keyword argument dictionaries are used to pass a variable number of keyword arguments to a function. The `**kwargs` parameter is used to collect all the keyword arguments passed to the function into a dictionary, which can then be accessed and processed inside the function.

## Example

```python
def process_data(name, *args, age=30, **kwargs):
    print("Name:", name)
    print("Age:", age)
    print("Positional arguments:")
    for arg in args:
        print(arg)
    print("Keyword arguments:")
    for key, value in kwargs.items():
        print(key, value)
```

In this function, we define a function `process_data()` that takes several different types of arguments:

- `name`: A required positional argument that must be passed to the function.
- `*args`: A variable-length argument list that collects any additional positional arguments passed to the function into a tuple.
- `age`: A default argument that is set to `30` if no value is passed for the `age` parameter.
- `**kwargs`: A variable-length keyword argument dictionary that collects any additional keyword arguments passed to the function into a dictionary.

Here's an example of calling the `process_data()` function using all the different argument passing methods:

```python
process_data("Alice", 1, 2, 3, age=25, city="New York", country="USA")
```

In this example, we call the `process_data()` function with the following arguments:

- `"Alice"`: A required positional argument that is passed first in the argument list.
- `1, 2, 3`: Additional positional arguments that are collected into the `args` tuple.
- `age=25`: A keyword argument that overrides the default value of `30` for the `age` parameter.
- `city="New York", country="USA"`: Additional keyword arguments that are collected into the `kwargs` dictionary.

When we call the `process_data()` function in this way, the function prints the following output:

```python
Name: Alice
Age: 25
Positional arguments:
1
2
3
Keyword arguments:
city New York
country USA
```

As you can see, the `process_data()` function is able to handle a variety of argument types, including required and optional positional arguments, default arguments, variable-length argument lists, and variable-length keyword argument dictionaries.

## slash syntax

> A slash in the argument list of a function denotes that the parameters prior to it are positional-only. Positional-only parameters are the ones without an externally-usable name. Upon calling a function that accepts positional-only parameters, arguments are mapped to parameters based solely on their position.
> [stackoverflow](https://stackoverflow.com/questions/24735311/what-does-the-slash-mean-when-help-is-listing-method-signatures)

In Python, the [slash (`/`)](https://docs.python.org/3/faq/programming.html#what-does-the-slash-in-the-parameter-list-of-a-function-mean) is a special syntax used to separate positional-only parameters from positional-or-keyword parameters in a function definition. The slash is used as a delimiter to indicate that all parameters listed before it are positional-only, meaning that they can only be passed as positional arguments and not as keyword arguments.

Here's an example of using the slash syntax in a Python function definition:

```python
def my_function(a, b, /, c, d):
    print("a =", a)
    print("b =", b)
    print("c =", c)
    print("d =", d)

my_function(1, 2, 3, 4)
```

In this example, we define a function `my_function()` that takes four parameters: `a`, `b`, `c`, and `d`. The slash syntax is used to indicate that the first two parameters, `a` and `b`, are positional-only, while the last two parameters, `c` and `d`, can be passed as either positional or keyword arguments.

When we call the `my_function()` function with the arguments `1`, `2`, `3`, and `4`, the first two arguments are passed as positional-only arguments and are matched to the `a` and `b` parameters, respectively. The last two arguments are passed as positional arguments and are matched to the `c` and `d` parameters, respectively.

```python
my_function(1, b=2, c=3, d=4)
# TypeError: my_function() got some positional-only arguments passed as keyword arguments: 'b'
my_function(1, 2, d=3, c=4)
# a = 1
# b = 2
# c = 4
# d = 3
```

The use of the slash syntax is mostly optional and depends on the specific requirements of the function. It can be useful in cases where you want to restrict certain parameters to be passed only as positional arguments, or when you want to make the function's interface more clear and self-documenting.

It's important to note that the slash syntax is only available in Python 3.8 and later versions. 

## asterisk (`*`)

Use asterisk (`*`) to specify keyword-only arguments.

```python
def my_function2(a, /, b, *, c, d):
    print("a =", a)
    print("b =", b)
    print("c =", c)
    print("d =", d)

my_function2(1, 2, c=3, d=4)
my_function2(1, b=2, c=3, d=4)
my_function2(a=1, b=2, c=3, d=4)
# TypeError: my_function2() got some positional-only arguments passed as keyword arguments: 'a'
my_function2(1, 2, 3, 4)
# TypeError: my_function3() takes 2 positional arguments but 4 were given
```

[pep 457](https://peps.python.org/pep-0457/)
