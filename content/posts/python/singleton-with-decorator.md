---
title: Singleton with Decorator
slug: singleton-with-decorator
author: aaron
date: 2023-05-04
tags: ["python", "singleton", "decorator", "design pattern"]
---


In Python, a singleton is a design pattern that restricts the instantiation of a class to a single object. A singleton class ensures that only one instance of the class is created and provides a global point of access to that instance.

One way to implement a singleton in Python is to use a decorator. Here's an example:

```python
def singleton(cls):
    instances = {}

    def get_instance(*args, **kwargs):
        if cls not in instances:
            instances[cls] = cls(*args, **kwargs)
        return instances[cls]

    return get_instance

@singleton
class MyClass:
    def __init__(self, x):
        self.x = x

my_obj1 = MyClass(42)
my_obj2 = MyClass(100)

print(my_obj1.x)  # Output: 42
print(my_obj2.x)  # Output: 42
print(my_obj1 is my_obj2)  # Output: True
```

In this example, the `singleton` decorator takes a class as an argument and returns a new function that acts as a factory for creating instances of the class. The `instances` dictionary is used to keep track of the instances created so far.

The `get_instance` function checks if an instance of the class already exists in the `instances` dictionary. If it does, it returns that instance. If not, it creates a new instance of the class and adds it to the `instances` dictionary before returning it.

Finally, the `@singleton` decorator is applied to the `MyClass` class, which wraps it with the `get_instance` function. This ensures that only one instance of `MyClass` is created and returned by the `get_instance` function.

When the `MyClass` constructor is called with different arguments to create `my_obj1` and `my_obj2` objects, the constructor initializes the `x` attribute of each object with the respective argument value. However, when we access the `x` attribute of `my_obj2`, we get the same value as `my_obj1`, because they are both instances of the same `MyClass` object.
