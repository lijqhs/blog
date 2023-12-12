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

The Facade pattern is a structural design pattern that provides a simplified interface to a complex subsystem of classes, making it easier to use and understand. It encapsulates the complexity of the subsystem behind a single interface, allowing clients to interact with the subsystem through a unified and simplified interface.

The Facade pattern can be related to other design patterns in the following ways:

1. Adapter Pattern: The Facade pattern can use the Adapter pattern to convert the interface of a complex subsystem into a simpler interface that clients can use. The Adapter pattern allows the Facade to work with existing subsystems that may have incompatible interfaces.

2. Composite Pattern: The Facade pattern can be used in conjunction with the Composite pattern to provide a unified interface to a composite structure. The Facade can encapsulate the complexity of interacting with the individual elements in the composite structure, providing a simplified interface to clients.

3. Singleton Pattern: The Facade pattern can use the Singleton pattern to ensure that there is only one instance of the Facade object. This can be useful when coordinating access to the complex subsystem and ensuring consistent behavior.

4. Mediator Pattern: The Facade pattern can be seen as a simplified form of the Mediator pattern. While the Mediator pattern focuses on coordinating communication between multiple objects, the Facade pattern focuses on providing a simplified interface to a subsystem.

5. Factory Pattern: The Facade pattern can work with the Factory pattern to provide a simplified way of creating complex objects or subsystems. The Facade can encapsulate the creation and initialization process, providing clients with a single interface to access the created objects.

It's important to note that the Facade pattern is primarily focused on simplifying and providing a unified interface to a complex subsystem. The choice of which patterns to use in conjunction with the Facade pattern depends on the specific requirements and complexity of the subsystem being encapsulated.