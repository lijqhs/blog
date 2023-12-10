---
title: Overriding vs. Overloading
slug: overriding-vs-overloading
author: aaron
date: 2023-05-12
tags: ["python", "overriding", "overloading", "object-oriented programming"]
---


Both overriding and overloading are concepts in object-oriented programming that allow you to define methods with the same name but different behavior. However, they differ in their implementation and purpose.

## Overriding

Overriding is a mechanism by which a subclass can provide a different implementation of a method that is already defined in its superclass. When a method is overridden, the subclass's implementation takes precedence over the superclass's implementation, allowing you to customize the behavior of the method for the specific subclass.

In Python, method overriding is achieved by defining a method with the same name as a method in the superclass. The subclass's method must have the same signature (i.e., the same name and parameters) as the superclass's method, but it can provide a different implementation.

Here's an example of method overriding in Python:

```python
class Animal:
    def make_sound(self):
        print("Generic animal sound")

class Dog(Animal):
    def make_sound(self):
        print("Woof")

animal = Animal()
dog = Dog()

animal.make_sound() # prints "Generic animal sound"
dog.make_sound() # prints "Woof"
```

In this example, we define a base class `Animal` with a `make_sound()` method that prints a generic animal sound. We then define a subclass `Dog` that overrides the `make_sound()` method with its own implementation that prints "Woof".

When we create an instance of the `Animal` class and call its `make_sound()` method, we get the generic animal sound. However, when we create an instance of the `Dog` class and call its `make_sound()` method, we get the "Woof" sound, because the subclass's implementation takes precedence over the superclass's implementation.

## Overloading

Overloading is a mechanism by which multiple methods can have the same name but different parameters. When a method is overloaded, the appropriate method to call is determined based on the number and types of arguments passed to it.

In Python, method overloading is not directly supported because Python allows methods to be called with any number and type of arguments. However, you can simulate method overloading by using default parameter values or variable-length argument lists.

Here's an example of simulating method overloading in Python using default parameter values:

```python
class Math:
    def add(self, a, b=None, c=None):
        if b is None and c is None:
            return a
        elif c is None:
            return a + b
        else:
            return a + b + c

math = Math()

print(math.add(2)) # prints 2
print(math.add(2, 3)) # prints 5
print(math.add(2, 3, 4)) # prints 9
```

In this example, we define a class `Math` with an `add()` method that can take one, two, or three parameters. If only one parameter is passed, the method returns that parameter. If two parameters are passed, the method returns their sum. If three parameters are passed, the method returns their sum.

By using default parameter values, we can simulate method overloading in Python, allowing the `add()` method to be called with different numbers of arguments.

Overall, while both overriding and overloading allow you to define methods with the same name but different behavior, they differ in their implementation and purpose. Overriding allows a subclass to provide a different implementation of a method defined in its superclass, while overloading allows multiple methods to have the same name but different parameters.
