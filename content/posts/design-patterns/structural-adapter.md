---
title: Adapter Pattern
slug: Adapter Pattern
author: aaron
date: 2023-05-20T10:10:00
series: ["Design Patterns"]
tags: ["adapter pattern", "bridge pattern", "proxy pattern", "facade pattern", "decorator pattern"]
---


The Adapter pattern is a structural design pattern that allows incompatible interfaces to work together by creating a bridge between them. It involves creating an adapter class that wraps an existing class and provides a compatible interface that other classes can use. This pattern is useful when you need to reuse existing classes that have different interfaces, or when you need to integrate third-party libraries into your application that have incompatible interfaces.

## Example

Here's an example of how to implement the Adapter pattern in Python:

```python
class Adaptee:
    def specific_request(self):
        return "Adaptee specific request"

class Target:
    def request(self):
        return "Target request"

class Adapter(Target):
    def __init__(self, adaptee):
        self._adaptee = adaptee
    
    def request(self):
        return self._adaptee.specific_request()

# Create an instance of the Adaptee class
adaptee = Adaptee()

# Create an instance of the Adapter class, wrapping the Adaptee instance
adapter = Adapter(adaptee)

# Call the request() method on the Adapter instance
result = adapter.request()

# Verify that the result is the same as calling specific_request() on the Adaptee instance
print(result == adaptee.specific_request())
```

Output:
```
True
```

Explanation:
- The `Adaptee` class is an existing class with a specific request interface that is incompatible with the `Target` class interface.
- The `Target` class is the target interface that the `Adapter` class needs to implement.
- The `Adapter` class wraps an instance of the `Adaptee` class and implements the `Target` interface by calling the `specific_request()` method on the `Adaptee` instance.
- In this example, we create an instance of the `Adaptee` class `adaptee`, create an instance of the `Adapter` class `adapter` that wraps the `adaptee` instance, and call the `request()` method on the `adapter` instance. We then verify that the result of calling `request()` on the `adapter` instance is the same as calling `specific_request()` on the `adaptee` instance.

## Pros of the Adapter pattern

- Allows incompatible interfaces to work together, which can help reuse existing code and integrate third-party libraries into your application.
- Provides a flexible way to add new functionality to an existing class without modifying its code.
- Can improve code readability by providing a more intuitive and consistent interface to other classes.

## Cons of the Adapter pattern

- Can add complexity to the code by introducing an additional layer of abstraction.
- Can reduce performance by adding extra method calls and object instantiations.
- Can make the code harder to understand and maintain if used excessively.

## When to use the Adapter pattern

- When you need to reuse existing classes that have incompatible interfaces.
- When you need to integrate third-party libraries into your application that have incompatible interfaces.
- When you need to add new functionality to an existing class without modifying its code.
- When you want to provide a more intuitive and consistent interface to other classes.

## Relations with other patterns

The Adapter pattern is a structural design pattern that allows objects with incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces, converting the interface of one class into another interface that clients expect. This pattern makes it possible for classes to work together that could not otherwise due to incompatible interfaces.

The Adapter pattern can be related to other design patterns in the following ways:

1. Decorator Pattern: Both the Adapter and Decorator patterns are structural patterns that wrap an object to modify its behavior. However, the main difference is their intent: the Adapter pattern is focused on providing a different interface, while the Decorator pattern adds additional responsibilities dynamically.

2. Bridge Pattern: The Bridge pattern also aims to decouple two incompatible interfaces, but it does so by separating the abstraction from its implementation. In contrast, the Adapter pattern focuses on adapting the interface of one class to another.

3. Proxy Pattern: The Proxy pattern provides a surrogate or placeholder for another object to control its access. While the Adapter pattern converts the interface of one object to match another, the Proxy pattern provides a level of indirection and control over the access to an object.

4. Facade Pattern: The Facade pattern provides a simplified interface to a complex subsystem, acting as a high-level interface that makes the subsystem easier to use. The Adapter pattern, on the other hand, provides a different interface for an existing class or object.

It's important to note that these patterns serve different purposes and can be used in combination to address various design challenges. The choice of which pattern to use depends on the specific requirements and constraints of the system being designed.
