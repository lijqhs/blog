---
title: Singleton
slug: Singleton
author: aaron
date: 2023-05-20T10:00:04
tags: ["python", "design pattern"]
---


The Singleton pattern is a creational design pattern that ensures that a class has only one instance and provides a global point of access to that instance. This pattern is useful when you need to limit the number of instances of a class to one, and when you want to provide a single point of access to that instance throughout your application.

## Example

Here's an example of how to implement the Singleton pattern in Python:

```python
class Singleton:
    _instance = None
    
    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

# Create two instances of the Singleton class
s1 = Singleton()
s2 = Singleton()

# Verify that the instances are the same object
print(s1 is s2)
# Output: True
```


Explanation:
- The `Singleton` class uses a private class variable `_instance` to store the single instance of the class.
- The `__new__()` method is overridden to ensure that only one instance of the class is created. If the `_instance` variable is `None`, a new instance is created and assigned to `_instance`. Otherwise, the existing instance is returned.
- In this example, we create two instances of the Singleton class `s1` and `s2`. Since the Singleton pattern ensures that only one instance of the class exists, `s1` and `s2` are the same object, as confirmed by the `is` operator.

## Pros of the Singleton pattern

- Ensures that only one instance of a class exists, which can help save memory and improve performance.
- Provides a global point of access to the instance, which can simplify object management and improve code readability.
- Can be implemented easily in many programming languages, including Python.

## Cons of the Singleton pattern

- Can be difficult to test, as it may be difficult to replace the Singleton object with a mock object for testing purposes.
- Can introduce global state into the application, which can make it harder to reason about and debug the code.
- Can violate the Single Responsibility Principle, as the Singleton class is responsible for managing the instance as well as its own functionality.

## When to use the Singleton pattern

- When you need to ensure that only one instance of a class exists, such as in the case of a database connection or a configuration manager.
- When you want to provide a single point of access to the instance throughout your application, which can simplify object management and improve code readability.
- When you want to save memory and improve performance by limiting the number of instances of a class.

## Relations with Other Patterns

The Singleton pattern is a creational design pattern that ensures the existence of only one instance of a class and provides global access to that instance. It is commonly used when you want to restrict the instantiation of a class to a single object throughout the application.

The Singleton pattern can be related to other design patterns in the following ways:

1. Factory Pattern: The Singleton pattern can be used together with the Factory pattern to ensure that only a single instance of a factory class is available. The Singleton can control the instantiation of the factory class and provide a global access point to it.

2. Proxy Pattern: The Singleton pattern can be used in conjunction with the Proxy pattern to create a single instance of a complex or resource-intensive object. The Proxy can act as a surrogate for the real object, providing additional functionality or controlling access to it.

3. Observer Pattern: The Singleton pattern can be used with the Observer pattern to implement a global event system or message bus. The Singleton instance can act as the central point for publishing and subscribing to events or messages.

4. Command Pattern: The Singleton pattern can be utilized with the Command pattern to create a single instance of a command processor or command registry. The Singleton ensures that there is only one instance managing the execution of commands throughout the application.

5. Monostate Pattern: The Monostate pattern is sometimes considered an alternative to the Singleton pattern. In the Monostate pattern, all instances of a class share the same internal state, giving the illusion of a Singleton-like behavior. However, each instance can be created separately, unlike the Singleton pattern.

It's important to note that while the Singleton pattern provides global access to a single instance, it should be used with caution as it can introduce tight coupling and hinder testability. It is essential to carefully consider the need for a Singleton and evaluate other alternatives based on the specific requirements of your application.