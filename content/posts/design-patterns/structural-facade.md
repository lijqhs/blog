---
title: Facade
slug: Facade
author: aaron
date: 2023-05-20T10:10:04
tags: ["python", "design pattern"]
---


The Facade pattern is a software design pattern that provides a simplified interface to a complex system of classes, interfaces, and objects. It is a structural pattern that is used to hide the complexities of a subsystem and provide a unified interface to the client.

The main idea behind the Facade pattern is to provide a **simplified, high-level interface** that shields the client from the details of the subsystem. The Facade object acts as a mediator between the client and the subsystem, and it provides a single point of entry to the subsystem's functionality.

Using the Facade pattern, you can simplify the interaction between the client and the subsystem by reducing the number of objects and interfaces that the client needs to deal with. This can help to improve the overall performance and maintainability of your code.

For example, imagine you have a complex system made up of multiple classes and interfaces. You could create a Facade object that provides a simplified interface to the client, allowing them to interact with the system without having to deal with all of the underlying complexity. The Facade object would handle all of the interactions with the subsystem and provide a simplified interface that the client can easily understand and use.

## Example

Sure, here's an example implementation of the Facade pattern in Python:

```python
# Subsystem classes
class SubsystemA:
    def operation_a(self):
        print("SubsystemA operation")

class SubsystemB:
    def operation_b(self):
        print("SubsystemB operation")

# Facade class
class Facade:
    def __init__(self):
        self._subsystem_a = SubsystemA()
        self._subsystem_b = SubsystemB()

    def operation(self):
        self._subsystem_a.operation_a()
        self._subsystem_b.operation_b()

# Client code
def client_code(facade: Facade):
    facade.operation()

# Usage
facade = Facade()
client_code(facade)
```

In this example, we have two subsystem classes (`SubsystemA` and `SubsystemB`) that perform different operations. We also have a Facade class that encapsulates the subsystems and provides a simplified interface (`operation`) to the client.

The `client_code` function takes a `Facade` object and calls its `operation` method, which in turn calls the methods of `SubsystemA` and `SubsystemB`.

When we create a `Facade` object and pass it to the `client_code` function, we get the output:

```
SubsystemA operation
SubsystemB operation
```

As you can see, the client interacts with the Facade object and doesn't have to deal with the complexities of the subsystems directly. Instead, the Facade object handles all of the interactions with the subsystems and provides a simplified interface to the client.

## Relations with Other Patterns

- **Facade** defines a new interface for existing objects, whereas **Adapter** tries to make the existing interface usable. Adapter usually wraps just one object, while Facade works with an entire subsystem of objects.

- **Abstract Factory** can serve as an alternative to **Facade** when you only want to hide the way the subsystem objects are created from the client code.

- **Flyweight** shows how to make lots of little objects, whereas **Facade** shows how to make a single object that represents an entire subsystem.

- **Facade** and **Mediator** have similar jobs: they try to organize collaboration between lots of tightly coupled classes.

    - *Facade* defines a simplified interface to a subsystem of objects, but it doesn’t introduce any new functionality. The subsystem itself is unaware of the facade. Objects within the subsystem can communicate directly.
    - *Mediator* centralizes communication between components of the system. The components only know about the mediator object and don’t communicate directly.
    A Facade class can often be transformed into a Singleton since a single facade object is sufficient in most cases.

- **Facade** is similar to **Proxy** in that both buffer a complex entity and initialize it on its own. Unlike Facade, *Proxy* has the same interface as its service object, which makes them interchangeable.
