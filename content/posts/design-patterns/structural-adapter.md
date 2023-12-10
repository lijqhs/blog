---
title: Adapter
slug: Adapter
author: aaron
date: 2023-05-20T10:10:00
tags: ["python", "design pattern"]
---


The Adapter pattern is a structural design pattern that allows incompatible interfaces to work together by creating a bridge between them. It involves creating an adapter class that wraps an existing class and provides a compatible interface that other classes can use. This pattern is useful when you need to reuse existing classes that have different interfaces, or when you need to integrate third-party libraries into your application that have incompatible interfaces.

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

Pros of the Adapter pattern:
- Allows incompatible interfaces to work together, which can help reuse existing code and integrate third-party libraries into your application.
- Provides a flexible way to add new functionality to an existing class without modifying its code.
- Can improve code readability by providing a more intuitive and consistent interface to other classes.

Cons of the Adapter pattern:
- Can add complexity to the code by introducing an additional layer of abstraction.
- Can reduce performance by adding extra method calls and object instantiations.
- Can make the code harder to understand and maintain if used excessively.

When to use the Adapter pattern:
- When you need to reuse existing classes that have incompatible interfaces.
- When you need to integrate third-party libraries into your application that have incompatible interfaces.
- When you need to add new functionality to an existing class without modifying its code.
- When you want to provide a more intuitive and consistent interface to other classes.

## Relations with Other Patterns

- Bridge is usually designed up-front, letting you develop parts of an application independently of each other. On the other hand, Adapter is commonly used with an existing app to make some otherwise-incompatible classes work together nicely.

- Adapter changes the interface of an existing object, while Decorator enhances an object without changing its interface. In addition, Decorator supports recursive composition, which isn’t possible when you use Adapter.

- Adapter provides a different interface to the wrapped object, Proxy provides it with the same interface, and Decorator provides it with an enhanced interface.

- Facade defines a new interface for existing objects, whereas Adapter tries to make the existing interface usable. Adapter usually wraps just one object, while Facade works with an entire subsystem of objects.

- Bridge, State, Strategy (and to some degree Adapter) have very similar structures. Indeed, all of these patterns are based on composition, which is delegating work to other objects. However, they all solve different problems. A pattern isn’t just a recipe for structuring your code in a specific way. It can also communicate to other developers the problem the pattern solves.

## Reference

- https://refactoring.guru/design-patterns/adapter
