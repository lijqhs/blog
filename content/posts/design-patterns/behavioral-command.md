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


## Pros of the Command pattern

1. It decouples the sender of a request from the object that performs the action, allowing for greater flexibility and extensibility.
2. It supports the implementation of undo/redo functionality by providing methods to execute and undo commands.
3. It enables the logging and queuing of requests, allowing for features like transactional behavior or command history.

## Cons of the Command pattern
1. The pattern can introduce a large number of command classes, which may increase code complexity.
2. It may not be suitable for commands that require direct communication or complex interactions between the sender and receiver.

## Related design patterns

1. Observer: The Command pattern is often used in conjunction with the Observer pattern, where the invoker sends commands to observers, and the observers carry out the commands. This allows for loosely coupled communication between the invoker and observers.
2. Memento: The Command pattern can be used with the Memento pattern to support undo/redo functionality. The Memento pattern can capture the state of the receiver before executing a command and restore it if needed for undoing the command.
