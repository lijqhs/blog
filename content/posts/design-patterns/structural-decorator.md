---
title: Decorator
slug: Decorator
author: aaron
date: 2023-05-20T10:10:03
tags: ["python", "design pattern"]
---


The Decorator pattern is a structural design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. It involves creating a decorator class that wraps an existing class and provides additional functionality, while still maintaining the original interface of the object. This pattern is useful when you need to add functionality to an object at runtime, or when you want to add functionality to a class without modifying its code.

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

Pros of the Decorator pattern:
- Allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class.
- Provides a flexible way to add new functionality to an object without modifying its code.
- Can improve code maintainability and readability by separating the concerns of different functionalities.

Cons of the Decorator pattern:
- Can add complexity to the code by introducing an additional layer of abstraction.
- Can reduce performance by adding extra method calls and object instantiations.
- Can make the code harder to understand and maintain if used excessively.

When to use the Decorator pattern:
- When you need to add functionality to an object at runtime.
- When you want to add functionality to a class without modifying its code.
- When you want to provide a flexible way to add new functionality to an object without modifying its code.
- When you want to separate the concerns of different functionalities.

## Relations with Other Patterns

- Adapter changes the interface of an existing object, while Decorator enhances an object without changing its interface. In addition, Decorator supports recursive composition, which isn’t possible when you use Adapter.

- Adapter provides a different interface to the wrapped object, Proxy provides it with the same interface, and Decorator provides it with an enhanced interface.

- Chain of Responsibility and Decorator have very similar class structures. Both patterns rely on recursive composition to pass the execution through a series of objects. However, there are several crucial differences.

  The CoR handlers can execute arbitrary operations independently of each other. They can also stop passing the request further at any point. On the other hand, various Decorators can extend the object’s behavior while keeping it consistent with the base interface. In addition, decorators aren’t allowed to break the flow of the request.

- Composite and Decorator have similar structure diagrams since both rely on recursive composition to organize an open-ended number of objects.

  A Decorator is like a Composite but only has one child component. There’s another significant difference: Decorator adds additional responsibilities to the wrapped object, while Composite just “sums up” its children’s results.

  However, the patterns can also cooperate: you can use Decorator to extend the behavior of a specific object in the Composite tree.

- Designs that make heavy use of Composite and Decorator can often benefit from using Prototype. Applying the pattern lets you clone complex structures instead of re-constructing them from scratch.

- Decorator lets you change the skin of an object, while Strategy lets you change the guts.

- Decorator and Proxy have similar structures, but very different intents. Both patterns are built on the composition principle, where one object is supposed to delegate some of the work to another. The difference is that a Proxy usually manages the life cycle of its service object on its own, whereas the composition of Decorators is always controlled by the client.

In summary, the Decorator pattern is useful when you need to add functionality to an object at runtime, or when you want to add functionality to a class without modifying its code. It can provide flexibility and improve code maintainability and readability, but can also add complexity and reduce performance if used excessively.
