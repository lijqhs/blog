---
title: Bridge Pattern
slug: Bridge Pattern
author: aaron
date: 2023-05-20T10:10:01
series: ["Design Patterns"]
# tags: ["bridge pattern", "adapter pattern", "composite pattern", "strategy pattern", "template method pattern", "decorator pattern"]
---


The Bridge pattern is a structural design pattern that decouples an abstraction from its implementation, allowing them to vary independently. It involves creating two separate hierarchies, one for the abstraction and one for the implementation, and using composition to link them together. This pattern is useful when you need to separate the interface of an object from its implementation, or when you need to support multiple implementations of an object.

## Example

Here's an example implementation of the Bridge Design Pattern in Python:

```python
# Define the abstraction interface
class Abstraction:
    def __init__(self, implementation):
        self.implementation = implementation

    def operation(self):
        self.implementation.operation_implementation()

# Define the implementation interface
class Implementation:
    def operation_implementation(self):
        pass

# Define the concrete implementation classes
class ConcreteImplementationA(Implementation):
    def operation_implementation(self):
        print("ConcreteImplementationA operation")

class ConcreteImplementationB(Implementation):
    def operation_implementation(self):
        print("ConcreteImplementationB operation")

# Use the abstraction and implementation
implementation_a = ConcreteImplementationA()
abstraction = Abstraction(implementation_a)
abstraction.operation()

implementation_b = ConcreteImplementationB()
abstraction = Abstraction(implementation_b)
abstraction.operation()
```

In this example, the `Abstraction` class defines the abstraction interface and holds a reference to an implementation object. The `Implementation` class defines the implementation interface, and the `ConcreteImplementationA` and `ConcreteImplementationB` classes provide the concrete implementations.

To use the abstraction and implementation, you create an instance of a concrete implementation and pass it to the `Abstraction` constructor. You can then call the `operation` method on the`Abstraction` object, which in turn calls the `operation_implementation` method on the implementation object.

In the example, we create an instance of `ConcreteImplementationA` and pass it to the `Abstraction` constructor, then call the `operation` method on the `abstraction` object, which prints "ConcreteImplementationA operation". We then create an instance of `ConcreteImplementationB` and repeat the process, which prints "ConcreteImplementationB operation". This shows how the abstraction and implementation can vary independently, allowing for greater flexibility and maintainability in our code.


## Use cases

The Bridge Design Pattern is a flexible pattern that can be used in many different scenarios where there is a need to separate an abstraction from its implementation. Here are some other use cases where the Bridge pattern can be applied:

1. User Interface Frameworks: In user interface frameworks, the Bridge pattern can be used to separate the user interface components from the platform-specific code that implements them. This allows for the user interface to be easily ported to different platforms without affecting the underlying components.

2. Database Access Layers: In database access layers, the Bridge pattern can be used to separate the database access code from the business logic code. This allows for changes to be made to the database implementation without affecting the business logic.

3. Graphic Rendering Libraries: In graphic rendering libraries, the Bridge pattern can be used to separate the rendering engine from the actual graphic objects being rendered. This allows for the rendering engine to be easily swapped out for a different one without affecting the graphic objects.

4. Audio/Video Streaming Services: In audio/video streaming services, the Bridge pattern can be used to separate the streaming protocol from the actual content being delivered. This allows for the service to be easily scaled to support different types of content and delivery methods.

5. Operating System APIs: In operating system APIs, the Bridge pattern can be used to separate the high-level API from the low-level system calls. This allows for the API to be easily ported to different operating systems without affecting the underlying system calls.

Overall, the Bridge patternis useful in any situation where there is a need to separate an abstraction from its implementation, allowing for greater flexibility and maintainability in the code.
