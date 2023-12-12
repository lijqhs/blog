---
title: Factory Method
slug: Factory Method
author: aaron
date: 2023-05-20T10:00:00
tags: ["python", "design pattern"]
---


> "Define an interface for creating an object, but let subclasses decide which class to instantiate. The Factory method lets a class defer instantiation it uses to subclasses." (Gang Of Four)

The Factory Method design pattern is a creational design pattern that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created. In other words, it encapsulates object creation and delegates it to subclasses, rather than instantiating objects directly in the superclass.

The Factory Method pattern is useful when you have a superclass that doesn't know what type of objects it needs to create, but it knows the type of objects it wants to use. The factory method can be used to create these objects without the superclass having to know exactly what type of object it needs to create.

## Example

I apologize for the confusion in my previous response. You are correct that my previous example did not demonstrate the Factory Method pattern correctly. Here is a corrected example:

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    @abstractmethod
    def speak(self):
        pass

class Dog(Animal):
    def speak(self):
        return "Woof!"

class Cat(Animal):
    def speak(self):
        return "Meow!"

class AnimalCreator(ABC):
    @abstractmethod
    def create_animal(self):
        pass

    def do_something(self):
        animal = self.create_animal()
        animal.speak()

class DogCreator(AnimalCreator):
    def create_animal(self):
        return Dog()

class CatCreator(AnimalCreator):
    def create_animal(self):
        return Cat()

# Usage
dog_creator = DogCreator()
cat_creator = CatCreator()

dog_creator.do_something()
cat_creator.do_something()

print(dog_creator.do_something())  # This will print "Woof!"
print(cat_creator.do_something())  # This will print "Meow!"
```

In this example, we have an abstract base class `Animal` that defines a method `speak()`. We also have two concrete classes `Dog` and `Cat` that implement the `speak()` method in their own way.

We also have an abstract class `AnimalCreator` that defines an factory method `create_animal()` and its business logic method `do_something` for its main purpose. The concrete `DogCreator` and `CatCreator` classes implement this method to create `Dog` and `Cat` objects, respectively.

>Note, despite its name, animal creation is not the primary responsibility of the creator. Usually, the creator class already has some core **business logic** related to products. The factory method helps to decouple this logic from the concrete product classes. Here is an analogy: a large software development company can have a training department for programmers. However, the primary function of the company as a whole is still writing code, not producing programmers.

## Pros and Cons

Pros:

- Encapsulates object creation: The Factory Method pattern encapsulates the object creation process in a separate class or method, which makes it easier to modify or extend the creation process without affecting the rest of the code.
- Provides flexibility and extensibility: By delegating object creation to subclasses, the Factory Method pattern allows for more flexibility and extensibility in the creation of objects, making it easier to add new types of objects in the future.
- Promotes loose coupling: The Factory Method pattern promotes loose coupling between classes by allowing them to communicate through interfaces rather than concrete implementations, which makes the code more modular and easier to maintain.
- Single Responsibility Principle. You can move the product creation code into one place in the program, making the code easier to support.
- Open/Closed Principle. You can introduce new types of products into the program without breaking existing client code.

Cons:

- Increased complexity: The Factory Method pattern can increase the complexity of the code by introducing additional classes and methods, which can be difficult to manage in large applications.
- Overhead: The Factory Method pattern can introduce additional overhead by requiring the creation of additional classes and methods, which can affect performance in applications with many objects.
- Requires more code: The Factory Method pattern requires the creation of additional classes and methods, which can result in more code that needs to be written and maintained.
- May not be necessary for simple applications: For simple applications with only a few types of objects, the Factory Method pattern may introduce unnecessary complexity and overhead.


## Related Design Patterns

The Factory Method pattern is a creational design pattern that defines an interface for creating objects, but lets subclasses decide which class to instantiate. It provides a way to delegate the instantiation logic to subclasses, allowing for flexible object creation.

The Factory Method pattern can be related to other design patterns in the following ways:

1. Abstract Factory Pattern: The Abstract Factory pattern provides an interface for creating families of related objects, while the Factory Method pattern focuses on creating a single object. The Factory Method can be used within an Abstract Factory to delegate the creation of individual objects to subclasses.

2. Singleton Pattern: The Factory Method pattern can be used in conjunction with the Singleton pattern to ensure that only one instance of a factory class is available. The Factory Method can encapsulate the logic for creating the Singleton instance and provide a centralized access point to it.

3. Template Method Pattern: The Factory Method pattern and the Template Method pattern are similar in that they both define a skeleton algorithm with certain steps that can be customized by subclasses. The Template Method pattern focuses on defining the overall algorithm, while the Factory Method pattern focuses on creating objects within that algorithm.

4. Strategy Pattern: The Factory Method pattern can be used in conjunction with the Strategy pattern to dynamically select and instantiate different strategies. The Factory Method can be used to create different strategy objects based on certain conditions or inputs.

5. Composite Pattern: The Factory Method pattern can be used with the Composite pattern to create composite objects. The Factory Method can be used to create the individual components of the composite and assemble them together.

It's important to note that the Factory Method pattern is primarily focused on creating objects in a flexible and extensible manner. The choice of which patterns to use in conjunction with the Factory Method pattern depends on the specific requirements and constraints of the system being designed.

## Reference

- https://en.wikipedia.org/wiki/Factory_method_pattern
- https://refactoring.guru/design-patterns/factory-method
- https://refactoring.guru/design-patterns/factory-method/python/example
- https://stackoverflow.com/a/5740020
