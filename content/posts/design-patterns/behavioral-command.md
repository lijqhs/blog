---
title: Command
slug: Command
author: aaron
date: 2023-05-20T10:20:01
tags: ["python", "design pattern"]
---


The Command pattern is a behavioral pattern that allows you to encapsulate a request as an object, thereby allowing you to parameterize clients with different requests, queue or log requests, and support undoable operations.

The main idea behind the Command pattern is to separate the object that invokes the operation from the object that knows how to perform the operation. This separation allows you to decouple the client that sends the request from the receiver that performs the request, and also allows you to implement the request as an object that can be passed as a parameter, stored, or manipulated like any other object.

Here's an example of the Command pattern in Python:

```python
# Command interface
class Command:
    def execute(self):
        pass

# Concrete command classes
class LightOnCommand(Command):
    def __init__(self, light):
        self._light = light

    def execute(self):
        self._light.turn_on()

class LightOffCommand(Command):
    def __init__(self, light):
        self._light = light

    def execute(self):
        self._light.turn_off()

# Receiver class
class Light:
    def turn_on(self):
        print("Light is on")

    def turn_off(self):
        print("Light is off")

# Invoker class
class Switch:
    def __init__(self, on_command, off_command):
        self._on_command = on_command
        self._off_command = off_command

    def turn_on(self):
        self._on_command.execute()

    def turn_off(self):
        self._off_command.execute()

# Client code
def client_code(switch: Switch):
    switch.turn_on()
    switch.turn_off()

# Usage
light = Light()
light_on_command = LightOnCommand(light)
light_off_command = LightOffCommand(light)
switch = Switch(light_on_command, light_off_command)
client_code(switch)
```

In this example, we have a `Command` interface that defines the common interface for both the `LightOnCommand` and `LightOffCommand` classes. The `LightOnCommand` and `LightOffCommand` classes represent the concrete commands that perform the "turn on" and "turn off" operations, respectively.

The `Light` class represents the receiver that knows how to perform the "turn on" and "turn off" operations.

The `Switch` class represents the invoker that knows how to execute the commands. The `Switch` class has an `on_command` attribute and an `off_command` attribute that represent the commands to execute when the switch is turned on and off, respectively.

When we create a `Switch` object with the `LightOnCommand` and `LightOffCommand` objects as parameters, and pass the `Switch` object to the `client_code` function, we get the output:

```
Light is on
Light is off
```

As you can see, the `Switch` object executes the `LightOnCommand` object when it is turned on, and executes the `LightOffCommand` object when it is turned off. This example demonstrates how the Command pattern can be used to encapsulate requests as objects, and decouple the object that invokes the operation from the object that knows how to perform the operation.

## Relations with Other Patterns

- Chain of Responsibility, Command, Mediator and Observer address various ways of connecting senders and receivers of requests:

  - Chain of Responsibility passes a request sequentially along a dynamic chain of potential receivers until one of them handles it.
  - Command establishes unidirectional connections between senders and receivers.
  - Mediator eliminates direct connections between senders and receivers, forcing them to communicate indirectly via a mediator object.
  - Observer lets receivers dynamically subscribe to and unsubscribe from receiving requests.

- Handlers in Chain of Responsibility can be implemented as Commands. In this case, you can execute a lot of different operations over the same context object, represented by a request.
  However, there’s another approach, where the request itself is a Command object. In this case, you can execute the same operation in a series of different contexts linked into a chain.

- You can use Command and Memento together when implementing “undo”. In this case, commands are responsible for performing various operations over a target object, while mementos save the state of that object just before a command gets executed.

- Command and Strategy may look similar because you can use both to parameterize an object with some action. However, they have very different intents.

  - You can use Command to convert any operation into an object. The operation’s parameters become fields of that object. The conversion lets you defer execution of the operation, queue it, store the history of commands, send commands to remote services, etc.

  - On the other hand, Strategy usually describes different ways of doing the same thing, letting you swap these algorithms within a single context class.

- Prototype can help when you need to save copies of Commands into history.

- You can treat Visitor as a powerful version of the Command pattern. Its objects can execute operations over various objects of different classes.
