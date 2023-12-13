---
title: Builder Pattern
slug: Builder Pattern 
author: aaron
date: 2023-05-20T10:00:02
series: ["Design Patterns"]
tags: ["builder pattern", "abstract factory pattern", "factory method pattern", "composite pattern"]
---


The Builder pattern is a creational design pattern that separates the construction of complex objects from their representation. It provides a step-by-step approach to building objects, allowing you to create different variations of an object while keeping the construction process consistent.

## Example

Here's an example of the Builder pattern implemented in Python:

```python
class Product:
    def __init__(self):
        self.part_a = None
        self.part_b = None

    def __str__(self):
        return f"Part A: {self.part_a}, Part B: {self.part_b}"


class Builder:
    def build_part_a(self):
        pass

    def build_part_b(self):
        pass

    def get_product(self):
        pass


class ConcreteBuilder(Builder):
    def __init__(self):
        self.product = Product()

    def build_part_a(self):
        self.product.part_a = "Part A"

    def build_part_b(self):
        self.product.part_b = "Part B"

    def get_product(self):
        return self.product


class Director:
    def __init__(self, builder):
        self.builder = builder

    def construct_product(self):
        self.builder.build_part_a()
        self.builder.build_part_b()


# Usage
builder = ConcreteBuilder()
director = Director(builder)
director.construct_product()
product = builder.get_product()
print(product)
```

In the example, we have a `Product` class that represents the object being built. The `Builder` class defines the interface for building the product, and the `ConcreteBuilder` class implements the specific construction steps. The `Director` class controls the construction process by invoking the builder's methods in a specific order.

## Pros of the Builder pattern

1. It provides a clear separation between the construction logic and the final object, making the construction process more manageable and flexible.
2. It allows you to create complex objects step by step, making it easier to handle variations and configurations.
3. It isolates the client code from the specifics of object construction, promoting loose coupling.

## Cons of the Builder pattern

1. The code complexity can increase due to the introduction of multiple classes and interfaces.
2. It may be less suitable for simpler object construction scenarios where the number of steps and variations is limited.

## Related design patterns

1. Factory Method: The Builder pattern can be seen as an alternative to the Factory Method pattern when the construction process involves multiple steps and variations.
2. Abstract Factory: The Builder pattern can be used together with the Abstract Factory pattern to create families of objects, with each builder representing a specific product family.
3. Composite: The Builder pattern can be combined with the Composite pattern to construct complex composite objects step by step.

These related patterns can complement the Builder pattern based on the specific requirements and design needs of the system.