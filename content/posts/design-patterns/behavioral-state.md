---
title: State
slug: State
author: aaron
date: 2023-05-20T10:20:06
tags: ["python", "design pattern"]
---


![problem](https://refactoring.guru/images/patterns/diagrams/state/problem1.png)

The State pattern is a behavioral pattern that allows an object to alter its behavior when its internal state changes. The pattern encapsulates state-dependent behavior into separate classes, and the object's behavior changes at runtime by switching between different state objects.

The main idea behind the State pattern is to provide a way to change an object's behavior without changing its class. Instead of using conditional statements to determine the behavior of an object based on its state, the State pattern uses a set of state classes that encapsulate the behavior and a context object that delegates to the current state.

## Example

Here's an example of the State pattern in Python:

```python
# State interface
class State:
    def handle(self, context):
        pass

# Concrete state classes
class ConcreteStateA(State):
    def handle(self, context):
        print("ConcreteStateA handling.")
        context.set_state(ConcreteStateB())

class ConcreteStateB(State):
    def handle(self, context):
        print("ConcreteStateB handling.")
        context.set_state(ConcreteStateA())

# Context class
class Context:
    def __init__(self):
        self._state = ConcreteStateA()

    def set_state(self, state):
        self._state = state

    def request(self):
        self._state.handle(self)

# Client code
def client_code():
    context = Context()

    context.request()
    context.request()
    context.request()
    context.request()

# Usage
client_code()
```

In this example, we have a `State` interface that defines the common interface for all the concrete state classes. The `State` object represents the state of the context object and encapsulates the behavior that is specific to that state.

The `ConcreteStateA` and `ConcreteStateB` classes are concrete state classes that implement the `State` interface. Each `ConcreteState` object encapsulates the behavior that is specific to that state.

The `Context` class is the object whose behavior changes as its internal state changes. The `Context` object maintains a reference to the current `State` object and delegates to it to handle requests.

When we create a `Context` object, change its state using the `set_state` method, and make requests using the `request` method, we get the output:

```
ConcreteStateA handling.
ConcreteStateB handling.
ConcreteStateA handling.
ConcreteStateB handling.
```

As you can see, the `Context` object's behavior changes as its internal state changes. The `Context` object delegates handling of requests to the current `State` object using the `handle` method. This example demonstrates how the State pattern can be used to encapsulate state-dependent behavior into separate classes, and the object's behavior changes at runtime by switching between different state objects.

## Pros of the State pattern

- It allows objects to change their behavior dynamically based on internal state changes, without the need for complex conditional statements or branching.
- It encapsulates state-specific behavior into separate classes, promoting code organization and modularity.
- It simplifies the addition of new states, as new state classes can be created without modifying existing code.

## Cons of the State pattern

- The number of classes can increase when multiple states are involved, potentially increasing the complexity of the codebase.
- Clients of the State pattern need to be aware of the available states and their transitions, which can introduce additional complexity.

## Related design patterns

1. Strategy: The State pattern is often considered a variation of the Strategy pattern. While both patterns encapsulate behavior into separate classes, the State pattern focuses on state-specific behavior and allows for dynamic state transitions.
2. State Machines: State Machines can be used in conjunction with the State pattern to define and manage state transitions in a more structured and formal way.

## Reference

- https://refactoring.guru/design-patterns/state
- https://en.wikipedia.org/wiki/Finite-state_machine

