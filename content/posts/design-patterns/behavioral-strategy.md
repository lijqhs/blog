---
title: Strategy Pattern
slug: Strategy Pattern
author: aaron
date: 2023-05-20T10:20:07
series: ["Design Patterns"]
# tags: ["strategy pattern", "template method pattern", "factory method pattern", "composite pattern"]
---


The Strategy pattern is a behavioral pattern that allows you to define a family of algorithms, encapsulate each one as an object, and make them interchangeable. The pattern allows you to vary the behavior of an object by selecting the appropriate algorithm at runtime.

The main idea behind the Strategy pattern is to provide a way to change an object's behavior without changing its implementation. Instead of implementing a single algorithm directly in the object, the Strategy pattern defines a set of algorithms as separate objects and allows the object to select the appropriate algorithm at runtime.

## Example

Here's an example of the Strategy pattern in Python:

```python
# Strategy interface
class Strategy:
    def do_algorithm(self, data):
        pass

# Concrete strategy classes
class ConcreteStrategyA(Strategy):
    def do_algorithm(self, data):
        return sorted(data)

class ConcreteStrategyB(Strategy):
    def do_algorithm(self, data):
        return reversed(sorted(data))

# Context class
class Context:
    def __init__(self, strategy):
        self._strategy = strategy

    def set_strategy(self, strategy):
        self._strategy = strategy

    def do_some_business_logic(self, data):
        result = self._strategy.do_algorithm(data)
        print(result)

# Client code
def client_code():
    context = Context(ConcreteStrategyA())
    context.do_some_business_logic([1, 4, 2, 5, 3])

    context.set_strategy(ConcreteStrategyB())
    context.do_some_business_logic([1, 4, 2, 5, 3])

# Usage
client_code()
```

In this example, we have a `Strategy` interface that defines the common interface for all the concrete strategy classes. The `Strategy` object represents an algorithm that can be used to perform a particular task.

The `ConcreteStrategyA` and `ConcreteStrategyB` classes are concrete strategy classes that implement the `Strategy` interface. Each `ConcreteStrategy` object encapsulates an algorithm that can be used to perform a particular task.

The `Context` class is the object that uses the algorithm to perform a particular task. The `Context` object maintains a reference to the current `Strategy` object and delegates to it to perform the algorithm.

When we create a `Context` object, change its strategy using the `set_strategy` method, and perform a task using the `do_some_business_logic` method, we get the output:

```
[1, 2, 3, 4, 5]
[5, 4, 3, 2, 1]
```

As you can see, the `Context` object's behavior changes as its internal strategy changes. The `Context` object delegates the algorithm to the current `Strategy` object using the `do_algorithm` method. This example demonstrates how the Strategy pattern can be used to define a family of algorithms, encapsulate each one as an object, and make them interchangeable.

## Pros of the Strategy pattern

- It enables you to encapsulate algorithms or behaviors into separate classes, promoting code organization and modularity.
- It allows for easy substitution of different strategies at runtime, making the system more flexible and adaptable.
- It avoids the need for conditional statements or branching based on different algorithms, improving code readability and maintainability.

## Cons of the Strategy pattern

- The number of classes can increase when multiple strategies are involved, potentially increasing the complexity of the codebase.
- Clients of the Strategy pattern need to be aware of the available strategies and select the appropriate one, which can introduce additional complexity.

## Related design patterns

1. Template Method: The Template Method pattern can be used in conjunction with the Strategy pattern to provide a common algorithm structure while allowing strategies to customize specific steps.
2. Factory Method: The Strategy pattern can be combined with the Factory Method pattern to encapsulate the creation of strategy objects and provide a centralized way to select and instantiate the appropriate strategy.
3. Composite: The Strategy pattern can be used in combination with the Composite pattern to apply strategies to a collection of objects hierarchically.