---
title: Chain of Responsibility
slug: Chain of Responsibility
author: aaron
date: 2023-05-20T10:20:00
tags: ["python", "design pattern"]
---


The Chain of Responsibility pattern is a behavioral pattern that allows you to create a chain of objects that can handle requests in a sequential order. Each object in the chain has the ability to handle the request, pass it on to the next object in the chain, or do both.

The main idea behind the Chain of Responsibility pattern is to decouple the sender of the request from the receiver by creating a chain of objects, each of which has the ability to handle the request. The sender of the request doesn't need to know which object in the chain will handle the request, and the receiver doesn't need to know who sent the request.

## Example 1

The Chain of Responsibility pattern is a behavioral pattern that allows you to create a chain of objects that can handle requests in a sequential order. Each object in the chain has the ability to handle the request, pass it on to the next object in the chain, or do both.

The main idea behind the Chain of Responsibility pattern is to decouple the sender of the request from the receiver by creating a chain of objects, each of which has the ability to handle the request. The sender of the request doesn't need to know which object in the chain will handle the request, and the receiver doesn't need to know who sent the request.

Here's an example of the Chain of Responsibility pattern in Python:

```python
# Handler interface
class Handler:
    def set_next(self, handler):
        pass

    def handle(self, request):
        pass

# Concrete handler classes
class ConcreteHandler1(Handler):
    def set_next(self, handler):
        self._next_handler = handler

    def handle(self, request):
        if request == "request1":
            print("ConcreteHandler1: Handling request1")
        else:
            self._next_handler.handle(request)

class ConcreteHandler2(Handler):
    def set_next(self, handler):
        self._next_handler = handler

    def handle(self, request):
        if request == "request2":
            print("ConcreteHandler2: Handling request2")
        else:
            self._next_handler.handle(request)

class ConcreteHandler3(Handler):
    def set_next(self, handler):
        self._next_handler = handler

    def handle(self, request):
        if request == "request3":
            print("ConcreteHandler3: Handling request3")
        else:
            print("End of chain. No handler found.")

# Client code
def client_code(handler: Handler):
    handler.handle("request1")
    handler.handle("request2")
    handler.handle("request3")

# Usage
handler1 = ConcreteHandler1()
handler2 = ConcreteHandler2()
handler3 = ConcreteHandler3()
handler1.set_next(handler2)
handler2.set_next(handler3)
client_code(handler1)
```

In this example, we have a `Handler` interface that defines the common interface for both the `ConcreteHandler` classes. The `ConcreteHandler` classes represent the concrete objects in the chain and implement the `handle` method to handle the request or pass it on to the next object in the chain.

The `ConcreteHandler` classes also have a `set_next` method that sets the next object in the chain. When the `handle` method is called, the class checks if it can handle the request. If it can, it handles the request. If it can't, it passes the request on to the next object in the chain by calling the `handle` method of the next object.

When we create a chain of `ConcreteHandler` objects, set the next object in the chain, and pass the first object in the chain to the `client_code` function, we get the output:

```
ConcreteHandler1: Handling request1
ConcreteHandler2: Handling request2
ConcreteHandler3: Handling request3
```

As you can see, each object in the chain handles the request it can handle, and passes the request on to the next object in the chain if it can't handle it. The last object in the chain returns a message indicating that the end of the chain has been reached.

This example demonstrates how the Chain of Responsibility pattern can be used to create a chain of objects that can handle requests in a sequential order, without the sender of the request needing to know which object in the chain will handle the request, and the receiver not needing to know who sent the request.

## Example 2

Let's say you are developing a helpdesk application that allows users to submit support tickets. When a user submits a support ticket, the application needs to route the ticket to the appropriate support team based on the type of issue. For example, network issues should be routed to the network team, software issues should be routed to the software team, and so on.

In this scenario, you could use the Chain of Responsibility pattern to create a chain of handlers that can route the support ticket to the appropriate team. Each handler in the chain represents a support team, and has the ability to handle the support ticket if it is a type of issue that the team is responsible for, or pass the support ticket on to the next handler in the chain if it is not.

Here's an example implementation of the Chain of Responsibility pattern in Python for this scenario:

```python
# Handler interface
class SupportHandler:
    def set_next(self, handler):
        pass

    def handle_request(self, request):
        pass

# Concrete handler classes
class NetworkSupportHandler(SupportHandler):
    def set_next(self, handler):
        self._next_handler = handler

    def handle_request(self, request):
        if request.type == "network":
            print("NetworkSupportHandler: Handling network issue")
            return True
        elif self._next_handler is not None:
            return self._next_handler.handle_request(request)
        else:
            return False

class SoftwareSupportHandler(SupportHandler):
    def set_next(self, handler):
        self._next_handler = handler

    def handle_request(self, request):
        if request.type == "software":
            print("SoftwareSupportHandler: Handling software issue")
            return True
        elif self._next_handler is not None:
            return self._next_handler.handle_request(request)
        else:
            return False

class HardwareSupportHandler(SupportHandler):
    def set_next(self, handler):
        self._next_handler = handler

    def handle_request(self, request):
        if request.type == "hardware":
            print("HardwareSupportHandler: Handling hardware issue")
            return True
        elif self._next_handler is not None:
            return self._next_handler.handle_request(request)
        else:
            return False

# Support ticket class
class SupportTicket:
    def __init__(self, type, description):
        self.type = type
        self.description = description

# Client code
def client_code(handler: SupportHandler, request: SupportTicket):
    if not handler.handle_request(request):
        print("No handler found.")

# Usage
network_handler = NetworkSupportHandler()
software_handler = SoftwareSupportHandler()
hardware_handler = HardwareSupportHandler()
network_handler.set_next(software_handler)
software_handler.set_next(hardware_handler)

request1 = SupportTicket("network", "Internet connection is down")
request2 = SupportTicket("software", "Application is crashing")
request3 = SupportTicket("hardware", "Laptop won't turn on")

client_code(network_handler, request1)
client_code(network_handler, request2)
client_code(network_handler, request3)
```

In this example, we have a `SupportHandler` interface that defines the common interface for all the `ConcreteHandler` classes. The `ConcreteHandler` classes represent the concrete objects in the chain and implement the `handle_request` method to handle the support ticket or pass it on to the next object in the chain.

The `SupportTicket` class represents a support ticket, and has a `type` attribute that specifies the type of issue, and a `description` attribute that provides a description of the issue.

When we create a chain of `ConcreteHandler` objects, set the next object in the chain, and pass the first object in the chain and a support ticket to the `client_code` function, we get the output:

```
NetworkSupportHandler: Handling network issue
SoftwareSupportHandler: Handling software issue
HardwareSupportHandler: Handling hardware issue
```

As you can see, each object in the chain handles the support ticket if it can handle the type of issue, and passes the support ticket on to the next object in the chain if it can't. The last object in the chain returns a message indicating that no handler was found. This example demonstrates how the Chain of Responsibility pattern can be used to create a chain of handlers that can route support tickets to the appropriate team based on the type of issue, without the sender of the ticket needing to know which handler in the chain will handle the ticket, and the receiver not needing to know who sent the ticket.
