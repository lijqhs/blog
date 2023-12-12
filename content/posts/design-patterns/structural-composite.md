---
title: Composite
slug: Composite
author: aaron
date: 2023-05-20T10:10:02
tags: ["python", "design pattern"]
---


The Composite pattern is a structural design pattern that allows you to compose objects into tree structures and represent part-whole hierarchies. It involves creating a common interface for both individual objects and groups of objects, and using recursion to traverse the object hierarchy. This pattern is useful when you need to work with complex hierarchies of objects and treat them uniformly.

## Example

Here's an example of how to implement the Composite pattern in Python:

```python
class Component:
    def operation(self):
        pass

class Leaf(Component):
    def operation(self):
        return "Leaf operation"

class Composite(Component):
    def __init__(self):
        self._children = []
    
    def add(self, component):
        self._children.append(component)
    
    def remove(self, component):
        self._children.remove(component)
    
    def operation(self):
        results = []
        for child in self._children:
            results.append(child.operation())
        return f"Composite operation: {', '.join(results)}"

# Create instances of the Leaf and Composite classes
leaf1 = Leaf()
leaf2 = Leaf()
composite = Composite()

# Add the Leaf instances to the Composite instance
composite.add(leaf1)
composite.add(leaf2)

# Call the operation() method on the Leaf and Composite instances
result_leaf = leaf1.operation()
result_composite = composite.operation()

# Verify that the results are different, indicating different types of objects
print(result_leaf != result_composite)
```

Output:
```
True
```

Explanation:
- The `Component` class is the base class for the object hierarchy, and defines the interface that all objects must implement.
- The `Leaf` class is a concrete implementation of the `Component` class, and represents the individual objects in the hierarchy.
- The `Composite` class is another concrete implementation of the `Component` class, and represents the groups of objects in the hierarchy. It contains a list of child components, and implements the `add()`, `remove()`, and `operation()` methods.
- In this example, we create instances of the `Leaf` and `Composite` classes, add the `Leaf` instances to the `Composite` instance, and call the `operation()` method on both instances. We then verify that the results are different, indicating that different types of objects are being accessed.

## Pros of the Composite pattern

- Allows you to work with complex hierarchies of objects and treat them uniformly, which can simplify your code and improve its readability.
- Provides a flexible way to add new objects to the hierarchy without changing the existing code.
- Can make it easy to implement recursive algorithms to traverse the object hierarchy.

## Cons of the Composite pattern

- Can add complexity to the code by introducing an additional layer of abstraction.
- Can reduce performance by adding extra method calls and object instantiations.
- Can make the code harder to understand and maintain if used excessively.

## When to use the Composite pattern

- When you need to work with complex hierarchies of objects and treat them uniformly.
- When you want to provide a flexible way to add new objects to the hierarchy without changing the existing code.
- When you need to implement recursive algorithms to traverse the object hierarchy.

## Relations with Other Patterns

The Composite pattern is a structural design pattern that allows you to compose objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly. In the Composite pattern, each element in the tree structure can be either a leaf node or a composite node.

The Composite pattern can be related to other design patterns in the following ways:

1. Iterator Pattern: The Composite pattern can work in conjunction with the Iterator pattern to provide a way to iterate over the elements in the composite structure. The Iterator pattern allows you to access the elements of an aggregate object sequentially without exposing its underlying representation.

2. Visitor Pattern: The Composite pattern can be used with the Visitor pattern to define operations that can be applied to elements in the composite structure. The Visitor pattern separates the operations from the structure, allowing new operations to be added without modifying the element classes.

3. Decorator Pattern: The Composite pattern can be combined with the Decorator pattern to add additional behavior or responsibilities to the individual elements in the composite structure. The Decorator pattern provides a way to dynamically add functionality to an object by wrapping it with one or more decorators.

4. Chain of Responsibility Pattern: The Composite pattern can be used in conjunction with the Chain of Responsibility pattern to create a hierarchical chain of responsibility. Each component in the composite structure can handle a request or pass it to the next component in the chain until it is processed.

5. Strategy Pattern: The Composite pattern can work with the Strategy pattern to encapsulate different algorithms or behaviors that can be applied to the elements in the composite structure. The Strategy pattern allows you to select an algorithm at runtime, providing flexibility and interchangeable behavior.

It's worth noting that these patterns serve different purposes and can be used in combination to solve different design problems. The choice of which patterns to use depends on the specific requirements and constraints of the system being designed.