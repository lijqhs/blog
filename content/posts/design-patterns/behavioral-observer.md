---
title: Observer Pattern
slug: Observer Pattern
author: aaron
date: 2023-05-20T10:20:05
series: ["Design Patterns"]
tags: ["observer pattern", "mediator pattern"]
---


![problem](https://refactoring.guru/images/patterns/content/observer/observer-comic-1-en.png)

The Observer pattern is a behavioral pattern that defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

The main idea behind the Observer pattern is to provide a way for objects to be notified of changes in the state of another object without tightly coupling them together. This allows for a more flexible and maintainable design by separating the concerns of the objects.

## Example

Here's an example of the Observer pattern in Python:

```python
# Observer interface
class Observer:
    def update(self, subject):
        pass

# Subject interface
class Subject:
    def attach(self, observer):
        pass

    def detach(self, observer):
        pass

    def notify(self):
        pass

# Concrete observer class
class ConcreteObserver(Observer):
    def update(self, subject):
        print("Subject state:", subject.get_state())

# Concrete subject class
class ConcreteSubject(Subject):
    def __init__(self):
        self._state = None
        self._observers = []

    def attach(self, observer):
        self._observers.append(observer)

    def detach(self, observer):
        self._observers.remove(observer)

    def notify(self):
        for observer in self._observers:
            observer.update(self)

    def set_state(self, state):
        self._state = state
        self.notify()

    def get_state(self):
        return self._state

# Client code
def client_code():
    subject = ConcreteSubject()
    observer1 = ConcreteObserver()
    observer2 = ConcreteObserver()

    subject.attach(observer1)
    subject.attach(observer2)

    subject.set_state("State 1")
    subject.set_state("State 2")

    subject.detach(observer2)

    subject.set_state("State 3")

# Usage
client_code()
```

In this example, we have an `Observer` interface that defines the common interface for all the concrete observer classes. The `Observer` object represents the object that is notified of changes in the state of the subject.

The `Subject` interface defines the common interface for all the concrete subject classes. The `Subject` object represents the object whose state is being observed and notifies its observers when its state changes.

The `ConcreteObserver` class is a concrete observer class that implements the `Observer` interface. The `ConcreteObserver` object represents an observer that is notified of changes in the state of the subject.

The `ConcreteSubject` class is a concrete subject class that implements the `Subject` interface. The `ConcreteSubject` object represents the object whose state is being observed and notifies its observers when its state changes.

When we create a `ConcreteSubject` object, create some `ConcreteObserver` objects, attach them to the subject using the `attach` method, change the subject's state using the `set_state` method, detach one of the observers using the `detach` method, and change the subject's state again, we get the output:

```
Subject state: State 1
Subject state: State 1
Subject state: State 2
Subject state: State 3
```

As you can see, the `ConcreteObserver` objects are notified of changes in the state of the `ConcreteSubject` object without tightly coupling them together. The `ConcreteSubject` object notifies its observers when its state changes using the `notify` method. This example demonstrates how the Observer pattern can be used to define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

## Pros of the Observer pattern

- It establishes a decoupled and flexible relationship between the subject and its observers, allowing for easy addition or removal of observers without modifying the subject.
- It enables the subject to notify multiple observers simultaneously, ensuring that they stay synchronized with the subject's state.
- It promotes the principle of separation of concerns by keeping the subject and observers separate, making the code easier to understand and maintain.

## Cons of the Observer pattern

- Observers may receive unnecessary notifications if the subject's state changes frequently or if the observers are not interested in all types of updates.
- Observers might have dependencies on the subject's implementation details, which can introduce tight coupling if not carefully designed.

## Related design patterns

1. Publisher/Subscriber: The Publisher/Subscriber pattern is an extension of the Observer pattern that introduces a central entity (the publisher) that manages the subscription and notification process between multiple publishers and subscribers. It provides more flexibility in terms of event filtering and multiple publishers.
2. Mediator: The Mediator pattern can be used in conjunction with the Observer pattern to decouple the communication between objects by introducing a mediator object that encapsulates the interaction logic between the subject and observers.
