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

## Relations with Other Patterns

- Bridge, State, Strategy (and to some degree Adapter) have very similar structures. Indeed, all of these patterns are based on composition, which is delegating work to other objects. However, they all solve different problems. A pattern isn’t just a recipe for structuring your code in a specific way. It can also communicate to other developers the problem the pattern solves.

- State can be considered as an extension of Strategy. Both patterns are based on composition: they change the behavior of the context by delegating some work to helper objects. Strategy makes these objects completely independent and unaware of each other. However, State doesn’t restrict dependencies between concrete states, letting them alter the state of the context at will.

## Reference

- https://refactoring.guru/design-patterns/state
- https://en.wikipedia.org/wiki/Finite-state_machine

