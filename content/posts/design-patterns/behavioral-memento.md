---
title: Memento Pattern
slug: Memento Pattern
author: aaron
date: 2023-05-20T10:20:04
series: ["Design Patterns"]
tags: ["memento pattern", "command pattern", "prototype pattern"]
---


![analogy](https://refactoring.guru/images/patterns/diagrams/memento/problem1-en.png)

The Memento pattern is a behavioral pattern that allows you to capture and externalize an object's internal state so that the object can be restored to that state later without violating encapsulation.

The main idea behind the Memento pattern is to provide a way to save and restore an object's state without exposing its internal structure. This allows you to save the state of an object at a particular point in time and restore it later if necessary.

## Example

Here's an example of the Memento pattern in Python:

```python
# Memento class
class Memento:
    def __init__(self, state):
        self._state = state

    def get_state(self):
        return self._state

# Originator class
class Originator:
    def __init__(self, state):
        self._state = state

    def create_memento(self):
        return Memento(self._state)

    def restore_memento(self, memento):
        self._state = memento.get_state()

    def get_state(self):
        return self._state

    def set_state(self, state):
        self._state = state

# Caretaker class
class Caretaker:
    def __init__(self, originator):
        self._originator = originator
        self._mementos = []

    def backup(self):
        self._mementos.append(self._originator.create_memento())

    def undo(self):
        if len(self._mementos) > 0:
            memento = self._mementos.pop()
            self._originator.restore_memento(memento)

# Client code
def client_code():
    originator = Originator("State 1")
    caretaker = Caretaker(originator)

    caretaker.backup()
    originator.set_state("State 2")

    caretaker.backup()
    originator.set_state("State 3")

    caretaker.undo()
    print(originator.get_state())

    caretaker.undo()
    print(originator.get_state())

# Usage
client_code()
```

In this example, we have a `Memento` class that represents the state of an object at a particular point in time. The `Memento` object encapsulates the object's internal state and provides a way to retrieve it later.

The `Originator` class is the object whose state is being saved and restored. The `Originator` object creates a `Memento` object to save its current state and restores its state from a `Memento` object.

The `Caretaker` class is responsible for managing the `Memento` objects. It stores the `Memento` objects in a list and provides methods for saving and restoring the `Originator` object's state.

When we create an `Originator` object, a `Caretaker` object, save the `Originator`'s state using the `backup` method, change the `Originator`'s state, and restore the `Originator`'s state using the `undo` method, we get the output:

```
State 2
State 1
```

As you can see, the `Caretaker` object manages the `Memento` objects and allows the `Originator` object's state to be saved and restored without exposing its internal structure. This example demonstrates how the Memento pattern can be used to capture and externalize an object's internal state so that the object can be restored to that state later without violating encapsulation.


## Pros of the Memento pattern

- It allows objects to save and restore their state without exposing internal details, maintaining encapsulation.
- It provides an easy way to implement undo/redo functionality or maintain checkpoints in an application.
- It promotes separation of concerns by separating the responsibility of state management from the object itself.

## Cons of the Memento pattern

- Storing and managing mementos can consume memory and impact performance, especially if a large number of mementos are created and stored.
- The pattern can become complex when dealing with objects with complex internal states.

## Related design patterns

1. Command: The Memento pattern can be used in conjunction with the Command pattern to support undo/redo functionality. The Command pattern can encapsulate operations and use the Memento pattern to capture and restore the state of objects affected by the operations.
2. Prototype: The Memento pattern can be used in conjunction with the Prototype pattern to create deep copies of objects and store their states as mementos.