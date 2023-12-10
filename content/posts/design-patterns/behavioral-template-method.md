---
title: Template Method
slug: Template Method
author: aaron
date: 2023-05-20T10:20:08
tags: ["python", "design pattern"]
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

## Relations with Other Patterns

- Factory Method is a specialization of Template Method. At the same time, a Factory Method may serve as a step in a large Template Method.

- Template Method is based on inheritance: it lets you alter parts of an algorithm by extending those parts in subclasses. Strategy is based on composition: you can alter parts of the object’s behavior by supplying it with different strategies that correspond to that behavior. Template Method works at the class level, so it’s static. Strategy works on the object level, letting you switch behaviors at runtime.
