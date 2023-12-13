---
title: Decorator Pattern
slug: Decorator Pattern
author: aaron
date: 2023-05-20T10:10:03
series: ["Design Patterns"]
# tags: ["decorator pattern", "adapter pattern", "composite pattern", "strategy pattern", "template method pattern", "proxy pattern"]
---


The Decorator pattern is a structural design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. It involves creating a decorator class that wraps an existing class and provides additional functionality, while still maintaining the original interface of the object. This pattern is useful when you need to add functionality to an object at runtime, or when you want to add functionality to a class without modifying its code.

## Example

Here's an example of how to implement the Decorator pattern in Python:

```python
class Component:
    def operation(self):
        pass

class ConcreteComponent(Component):
    def operation(self):
        return "ConcreteComponent operation"

class Decorator(Component):
    def __init__(self, component):
        self._component = component
    
    def operation(self):
        return self._component.operation()

class ConcreteDecoratorA(Decorator):
    def operation(self):
        return f"ConcreteDecoratorA operation, {self._component.operation()}"

class ConcreteDecoratorB(Decorator):
    def operation(self):
        return f"ConcreteDecoratorB operation, {self._component.operation()}"

# Create an instance of the ConcreteComponent class
component = ConcreteComponent()

# Create instances of the ConcreteDecoratorA and ConcreteDecoratorB classes, wrapping the ConcreteComponent instance
decorator_a = ConcreteDecoratorA(component)
decorator_b = ConcreteDecoratorB(component)

# Call the operation() method on the Decorator instances
result_a = decorator_a.operation()
result_b = decorator_b.operation()

# Verify that the results are different, indicating different decorators
print(result_a != result_b)
```

Output:
```
True
```

Explanation:
- The `Component` class is the base class for the object hierarchy, and defines the interface that all objects must implement.
- The `ConcreteComponent` class is a concrete implementation of the `Component` class, and represents the original object to be decorated.
- The `Decorator` class is the base class for all decorators, and contains a reference to an instance of the `Component` class.
- The `ConcreteDecoratorA` and `ConcreteDecoratorB` classes are concrete decorators that add additional functionality to the original object.
- In this example, we create an instance of the `ConcreteComponent` class `component`, create instances of the `ConcreteDecoratorA` and `ConcreteDecoratorB` classes that wrap the `component` instance, and call the `operation()` method on both instances. We then verify that the results are different, indicating that different decorators are being used.

## Pros of the Decorator pattern

- Allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class.
- Provides a flexible way to add new functionality to an object without modifying its code.
- Can improve code maintainability and readability by separating the concerns of different functionalities.

## Cons of the Decorator pattern

- Can add complexity to the code by introducing an additional layer of abstraction.
- Can reduce performance by adding extra method calls and object instantiations.
- Can make the code harder to understand and maintain if used excessively.

## When to use the Decorator pattern

- When you need to add functionality to an object at runtime.
- When you want to add functionality to a class without modifying its code.
- When you want to provide a flexible way to add new functionality to an object without modifying its code.
- When you want to separate the concerns of different functionalities.

## Relations with Other Patterns

The Decorator pattern is a structural design pattern that allows behavior to be added to an individual object dynamically, without affecting the behavior of other objects of the same class. It provides a flexible alternative to subclassing for extending functionality.

The Decorator pattern can be related to other design patterns in the following ways:

1. Adapter Pattern: The Decorator pattern and Adapter pattern both involve wrapping an object with additional functionality. However, the intent of the Adapter pattern is to provide a different interface to an existing object, while the Decorator pattern adds new behavior or responsibilities to an object without changing its interface.

2. Composite Pattern: The Decorator pattern can be used in conjunction with the Composite pattern to add additional behavior to individual elements in a composite structure. The Decorator pattern allows you to dynamically add responsibilities to objects, while the Composite pattern allows you to treat individual objects and compositions uniformly.

3. Strategy Pattern: The Decorator pattern can be used with the Strategy pattern to provide multiple ways of extending or modifying an object's behavior. The Strategy pattern defines a family of algorithms, encapsulates each one, and makes them interchangeable. The Decorator pattern can then be used to dynamically apply different strategies to an object.

4. Template Method Pattern: The Decorator pattern can be seen as an alternative to the Template Method pattern for extending the behavior of a class. The Template Method pattern defines a skeleton of an algorithm in a base class, allowing subclasses to provide specific implementations for certain steps. The Decorator pattern, on the other hand, allows behavior to be added dynamically to an object at runtime.

5. Proxy Pattern: The Decorator pattern can be similar to the Proxy pattern in that both involve wrapping an object. However, the Proxy pattern is focused on controlling access to the object, while the Decorator pattern is focused on adding new behavior or responsibilities to the object.

It's important to note that these patterns serve different purposes and can be used in combination to address various design challenges. The choice of which pattern to use depends on the specific requirements and constraints of the system being designed.