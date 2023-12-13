---
title: Template Method Pattern
slug: Template Method Pattern
author: aaron
date: 2023-05-20T10:20:08
series: ["Design Patterns"]
tags: ["template method pattern", "factory method pattern", "strategy pattern"]
---


The Template Method pattern is a behavioral pattern that defines the basic steps of an algorithm and allows subclasses to override some of the steps without changing the algorithm's structure. The pattern defines a skeleton of an algorithm in a base class and allows subclasses to implement the details of the algorithm in their own way.

The main idea behind the Template Method pattern is to provide a way to define a common algorithm structure that can be reused across different subclasses, while still allowing the subclasses to customize some parts of the algorithm's behavior.

## Example

Here's an example of the Template Method pattern in Python:

```python
# Abstract class with template method
class AbstractClass:
    def template_method(self):
        self.do_step_one()
        self.do_step_two()
        self.do_step_three()

    def do_step_one(self):
        raise NotImplementedError()

    def do_step_two(self):
        raise NotImplementedError()

    def do_step_three(self):
        raise NotImplementedError()

# Concrete class implementing template method
class ConcreteClass(AbstractClass):
    def do_step_one(self):
        print("Doing step one in ConcreteClass.")

    def do_step_two(self):
        print("Doing step two in ConcreteClass.")

    def do_step_three(self):
        print("Doing step three in ConcreteClass.")

# Client code
def client_code():
    concrete = ConcreteClass()
    concrete.template_method()

# Usage
client_code()
```

In this example, we have an `AbstractClass` that defines the common algorithm structure using a template method called `template_method`. The `AbstractClass` object represents the basic skeleton of the algorithm and provides default implementations for some steps.

The `ConcreteClass` is a concrete class that inherits from the `AbstractClass` and provides specific implementations for the abstract methods `do_step_one`, `do_step_two`, and `do_step_three`. The `ConcreteClass` object represents a specific implementation of the algorithm.

When we create a `ConcreteClass` object and call its `template_method` method, we get the output:

```
Doing step one in ConcreteClass.
Doing step two in ConcreteClass.
Doing step three in ConcreteClass.
```

As you can see, the `ConcreteClass` object follows the common algorithm structure defined in the `AbstractClass` and provides specific implementations for some of the steps. This example demonstrates how the Template Method pattern can be used to define a common algorithm structure that can be reused across different subclasses, while still allowing the subclasses to customize some parts of the algorithm's behavior.


## Pros of the Template Method pattern

- It promotes code reuse by providing a common algorithm structure in the base class and allowing subclasses to customize specific parts.
- It provides a clear separation between the overall algorithm and the specific implementations, making the code easier to understand and maintain.
- It allows for extension without modification, as new subclasses can be created to introduce new variations of the algorithm.

## Cons of the Template Method pattern

- It can make the code more complex by adding an additional layer of abstraction and inheritance.
- It may limit flexibility compared to other patterns that allow more dynamic composition of behavior.

## Related design patterns

1. Strategy Pattern: The Template Method pattern can be contrasted with the Strategy pattern. While the Template Method uses inheritance to define the algorithm structure, the Strategy pattern uses composition by encapsulating algorithms in separate classes and allowing them to be switched at runtime.
2. Hook Method: A Hook Method is a special method in the Template Method pattern that provides a default implementation but can be overridden by subclasses to customize behavior at certain points in the algorithm.
3. Factory Method: The Template Method pattern can be combined with the Factory Method pattern to provide a common algorithm structure for creating objects, while delegating the creation of specific objects to subclasses.
