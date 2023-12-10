---
title: Monkey Patching
slug: monkey-patching
author: aaron
date: 2023-05-09
tags: ["python", "monkey patching"]
---


In Python programming, monkey patching refers to the practice of modifying or extending the behavior of a module or object at runtime. This technique allows developers to change the behavior of existing code without modifying the original source code. While monkey patching can be a powerful tool, it can also be dangerous if used improperly. 

## What is Monkey Patching?

Monkey patching is a technique that allows developers to dynamically modify the behavior of an object or module at runtime. Essentially, it involves changing the code of an existing object or function without modifying the original source code. This can be useful in situations where you need to add functionality to an existing system, or when you need to fix a bug in a third-party library.

## How does it work?

In Python, everything is an object, including modules, classes, and functions. This means that you can modify their behavior by changing their attributes or methods. Monkey patching involves replacing an existing attribute or method with a new one at runtime. For example, you might replace a method in a third-party library with a custom implementation that fixes a bug or adds new functionality.

## Why use Monkey Patching?

There are several reasons why you might want to use monkey patching in your Python code. Here are a few examples:

1. Fixing bugs in third-party libraries: If you're using a third-party library that has a bug, you can use monkey patching to fix the bug without waiting for the library's developers to release a new version.

2. Adding functionality to existing code: If you need to add new functionality to an existing system, you can use monkey patching to add the new functionality without modifying the original source code.

3. Testing: In some cases, you may want to test a specific part of your code without running the entire program. Monkey patching can be used to replace an object or function with a mock object or function for testing purposes.

## Examples of Monkey Patching in Python

### Example 1: Fixing a bug in a third-party library

Suppose you're using a third-party library that has a bug in one of its methods. You can use monkey patching to fix the bug without modifying the original source code. Here's an example:

```python
import third_party_library

def new_method(self, arg1, arg2):
    # Fix bug in original method
    pass

# Monkey patch the library's method with our new method
third_party_library.original_method = new_method
```

In this example, we import the third-party library and define a new method that fixes the bug in the original method. We then replace the original method with our new method using monkey patching.

### Example 2: Adding functionality to an existing class

Suppose you're working with an existing class that doesn't have a method you need. You can use monkey patching to add the method at runtime.

```python
class MyClass:
    def existing_method(self):
        pass

# Add a new method to MyClass using monkey patching
def new_method(self):
    # New functionality
    pass

MyClass.new_method = new_method
```

In this example, we define a new method and add it to the `MyClass` class using monkey patching.

### Example 3: Mocking a function for testing

Suppose you're writing unit tests for a function that depends on another function that is slow or has side effects. You can use monkey patching to replace the slow or side-effectful function with a mock function that returns predictable results. Here's an example:

```python
def slow_function():
    # This function takes a long time to run
    pass

def my_function():
    # Do some work
    result = slow_function()
    # Do some more work
    return result

# Mock the slow function for testing
def mock_function():
    return "mock result"

# Monkey patch the slow function with the mock function
slow_function = mock_function

# Test my_function with the mock function
assert my_function() == "mock result"
```

In this example, we define a slow function and a function that depends on it. We then define a mock function that returns a predictable result and use monkey patching to replace the slow function with the mock function for testing purposes.

## When Not to Use Monkey Patching

While monkey patching can be a powerful tool in certain situations, there are also situations where it's better to avoid using this technique. Here are some situations where you should avoid using monkey patching:

1. Third-Party Code
If you're working with third-party code, it's generally better to avoid monkey patching. Modifying the behavior of third-party code can cause unintended side effects that can be hard to debug and maintain.

2. Production Code
Monkey patching is generally not recommended in production code, where reliability and maintainability are critical. If you need to modify the behavior of an object or module in production code, it's better to modify the source code directly or use a subclass or wrapper instead.

3. Large Codebases
Monkey patching can be more difficult to manage in large codebases, where it's harder to keep track of all the modifications that have been made. If you're working with a large codebase, it's better to avoid monkey patching and modify the source code directly or use a subclass or wrapper instead.

4. Testing
While monkey patching can be useful for testing, it's important to use it judiciously. If you're not careful, you can end up with test code that's hard to understand and maintain. It's better to use monkey patching sparingly and only when it's necessary.
