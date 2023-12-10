---
title: Composite
slug: Composite
author: aaron
date: 2023-05-20T10:10:02
tags: ["python", "design pattern"]
---


The Composite pattern is a structural design pattern that allows you to compose objects into tree structures and represent part-whole hierarchies. It involves creating a common interface for both individual objects and groups of objects, and using recursion to traverse the object hierarchy. This pattern is useful when you need to work with complex hierarchies of objects and treat them uniformly.

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

Pros of the Composite pattern:
- Allows you to work with complex hierarchies of objects and treat them uniformly, which can simplify your code and improve its readability.
- Provides a flexible way to add new objects to the hierarchy without changing the existing code.
- Can make it easy to implement recursive algorithms to traverse the object hierarchy.

Cons of the Composite pattern:
- Can add complexity to the code by introducing an additional layer of abstraction.
- Can reduce performance by adding extra method calls and object instantiations.
- Can make the code harder to understand and maintain if used excessively.

When to use the Composite pattern:
- When you need to work with complex hierarchies of objects and treat them uniformly.
- When you want to provide a flexible way to add new objects to the hierarchy without changing the existing code.
- When you need to implement recursive algorithms to traverse the object hierarchy.

## Relations with Other Patterns

- You can use Builder when creating complex Composite trees because you can program its construction steps to work recursively.

- Chain of Responsibility is often used in conjunction with Composite. In this case, when a leaf component gets a request, it may pass it through the chain of all of the parent components down to the root of the object tree.

- You can use Iterators to traverse Composite trees.

- You can use Visitor to execute an operation over an entire Composite tree.

- You can implement shared leaf nodes of the Composite tree as Flyweights to save some RAM.

- Composite and Decorator have similar structure diagrams since both rely on recursive composition to organize an open-ended number of objects.

  A Decorator is like a Composite but only has one child component. There’s another significant difference: Decorator adds additional responsibilities to the wrapped object, while Composite just “sums up” its children’s results.

  However, the patterns can also cooperate: you can use Decorator to extend the behavior of a specific object in the Composite tree.

- Designs that make heavy use of Composite and Decorator can often benefit from using Prototype. Applying the pattern lets you clone complex structures instead of re-constructing them from scratch.

In summary, the Composite pattern is useful when you need to work with complex hierarchies of objects and treat them uniformly. It can simplify your code and improve its readability, but can also add complexity and reduce performance if used excessively.
