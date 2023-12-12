---
title: Iterator
slug: Iterator
author: aaron
date: 2023-05-20T10:20:02
tags: ["python", "design pattern"]
---


The Iterator pattern is a behavioral pattern that provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

The main idea behind the Iterator pattern is to provide a uniform interface for traversing different types of collections, such as arrays, lists, trees, and so on. This interface allows clients to iterate over the elements of a collection without having to know about the internal structure of the collection.

## Example

Here's an example of the Iterator pattern in Python:

```python
# Iterator interface
class Iterator:
    def __init__(self, collection):
        self._collection = collection
        self._index = 0

    def __next__(self):
        if self._index < len(self._collection):
            value = self._collection[self._index]
            self._index += 1
            return value
        else:
            raise StopIteration

# Aggregate interface
class Aggregate:
    def create_iterator(self):
        pass

# Concrete aggregate class
class ListAggregate(Aggregate):
    def __init__(self):
        self._list = []

    def add(self, value):
        self._list.append(value)

    def create_iterator(self):
        return Iterator(self._list)

# Client code
def client_code(iterator: Iterator):
    while True:
        try:
            value = next(iterator)
            print(value)
        except StopIteration:
            break

# Usage
list_aggregate = ListAggregate()
list_aggregate.add("Item 1")
list_aggregate.add("Item 2")
list_aggregate.add("Item 3")
iterator = list_aggregate.create_iterator()
client_code(iterator)
```

In this example, we have an `Iterator` interface that defines the common interface for all the concrete iterator classes. The `Iterator` object represents an iterator that can traverse the elements of a collection.

The `Aggregate` interface defines the common interface for all the concrete aggregate classes. The `Aggregate` object represents the collection that can be iterated over.

The `ListAggregate` class is a concrete aggregate class that implements the `Aggregate` interface. The `ListAggregate` class represents a list that can be iterated over.

When we create a `ListAggregate` object, add some items to it, create an iterator using the `create_iterator` method, and pass the iterator to the `client_code` function, we get the output:

```
Item 1
Item 2
Item 3
```

As you can see, the `client_code` function iterates over the elements of the list using the `next` method of the iterator. The iterator provides a uniform interface for traversing the list without exposing its underlying representation. This example demonstrates how the Iterator pattern can be used to provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.


## Pros of the Iterator pattern

1. It provides a uniform way to iterate over different types of collections without exposing their internal structure or implementation details.
2. It simplifies the client code by abstracting the traversal logic and providing a consistent interface for accessing elements.
3. It supports multiple iterations over the same collection simultaneously.

## Cons of the Iterator pattern

1. It adds an additional layer of abstraction, which can increase the complexity of the code.
2. The iterator may not be efficient for certain types of collections, especially if the collection needs to be modified during iteration.

## Related design patterns

1. Composite: The Iterator pattern is often used in conjunction with the Composite pattern to iterate over composite structures, such as trees or hierarchies, where the iterator traverses the structure and provides a way to access the individual elements.
2. Factory Method: The Factory Method pattern can be used to provide a standardized way to create iterators for different types of collections, encapsulating the creation logic and allowing for more flexibility and extensibility.
