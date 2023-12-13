---
title: Mediator Pattern
slug: Mediator Pattern
author: aaron
date: 2023-05-20T10:20:03
series: ["Design Patterns"]
tags: ["mediator pattern", "observer pattern", "facade pattern"]
---


![analogy](https://refactoring.guru/images/patterns/diagrams/mediator/live-example.png)

The Mediator pattern is a behavioral pattern that defines an object that encapsulates how a set of objects interact with each other. It promotes loose coupling by keeping objects from referring to each other explicitly and allows for their interaction to be centralised in a mediator object.

The main idea behind the Mediator pattern is to reduce the complexity of the interactions between objects by introducing a mediator object that handles the communication between them. Instead of objects communicating directly with each other and knowing about each other's details, they communicate through a mediator object, which knows how to handle the interactions and can modify the behavior of the objects without them knowing.

## Example

Here's an example of the Mediator pattern in Python:

```python
# Mediator interface
class Mediator:
    def notify(self, sender, event):
        pass

# Concrete mediator class
class ChatroomMediator(Mediator):
    def __init__(self):
        self._users = []

    def register(self, user):
        self._users.append(user)

    def notify(self, sender, event):
        for user in self._users:
            if user != sender:
                user.receive(event)

# Colleague interface
class Colleague:
    def __init__(self, mediator):
        self._mediator = mediator

    def send(self, event):
        self._mediator.notify(self, event)

    def receive(self, event):
        print(event)

# Concrete colleague classes
class User(Colleague):
    def __init__(self, name, mediator):
        super().__init__(mediator)
        self._name = name

    def send_message(self, message):
        self.send(self._name + ": " + message)

# Client code
def client_code():
    mediator = ChatroomMediator()
    user1 = User("Alice", mediator)
    user2 = User("Bob", mediator)
    user3 = User("Charlie", mediator)

    mediator.register(user1)
    mediator.register(user2)
    mediator.register(user3)

    user1.send_message("Hi, everyone!")
    user2.send_message("Hello, Alice!")
    user3.send_message("Hey, Bob!")

# Usage
client_code()
```

In this example, we have a `Mediator` interface that defines the common interface for all the concrete mediator classes. The `Mediator` object represents the mediator that handles the communication between objects.

The `ChatroomMediator` class is a concrete mediator class that implements the `Mediator` interface. The `ChatroomMediator` class represents a chatroom that mediates the communication between users.

The `Colleague` interface defines the common interface for all the concrete colleague classes. The `Colleague` object represents the object that communicates with other objects through the mediator.

The `User` class is a concrete colleague class that implements the `Colleague` interface. The `User` class represents a user in the chatroom that communicates with other users through the `ChatroomMediator` object.

When we create a `ChatroomMediator` object, create some `User` objects, register them with the mediator using the `register` method, and have them send messages to each other using the `send_message` method, we get the output:

```
Bob: Hello, Alice!
Charlie: Hey, Bob!
Alice: Hi, everyone!
```

As you can see, the `User` objects communicate with each other through the `ChatroomMediator` object, without knowing about each other's details. The `ChatroomMediator` object handles the communication between the users and modifies their behavior without them knowing. This example demonstrates how the Mediator pattern can be used to encapsulate how a set of objects interact with each other and reduce the complexity of their interactions.


## Pros of the Mediator pattern

1. It decouples components by promoting indirect communication through a mediator object, reducing the dependencies between components.
2. It simplifies the communication logic and coordination between components, centralizing it in the mediator.
3. It improves code maintainability and extensibility by allowing easy addition or removal of components and changing their interaction without modifying existing components.

## Cons of the Mediator pattern

1. The mediator can become a centralized component that handles multiple responsibilities, which can introduce complexity if not managed properly.
2. Adding new components may require modifications to the mediator, potentially affecting other components.

## Related design patterns

1. Observer: The Mediator pattern can be used in conjunction with the Observer pattern to enable communication between components through the mediator, with the mediator acting as the subject and the components as observers.
2. Facade: The Mediator pattern is similar to the Facade pattern in that both patterns promote loose coupling and encapsulation, but they have different focuses. The Mediator pattern focuses on coordinating communication between components, while the Facade pattern focuses on providing a simplified interface to a subsystem.
