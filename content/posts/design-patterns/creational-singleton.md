---
title: Singleton
slug: Singleton
author: aaron
date: 2023-05-20T10:00:04
tags: ["python", "design pattern"]
---


The Singleton pattern is a creational design pattern that ensures that a class has only one instance and provides a global point of access to that instance. This pattern is useful when you need to limit the number of instances of a class to one, and when you want to provide a single point of access to that instance throughout your application.

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

Pros of the Singleton pattern:
- Ensures that only one instance of a class exists, which can help save memory and improve performance.
- Provides a global point of access to the instance, which can simplify object management and improve code readability.
- Can be implemented easily in many programming languages, including Python.

Cons of the Singleton pattern:
- Can be difficult to test, as it may be difficult to replace the Singleton object with a mock object for testing purposes.
- Can introduce global state into the application, which can make it harder to reason about and debug the code.
- Can violate the Single Responsibility Principle, as the Singleton class is responsible for managing the instance as well as its own functionality.

When to use the Singleton pattern:
- When you need to ensure that only one instance of a class exists, such as in the case of a database connection or a configuration manager.
- When you want to provide a single point of access to the instance throughout your application, which can simplify object management and improve code readability.
- When you want to save memory and improve performance by limiting the number of instances of a class.
