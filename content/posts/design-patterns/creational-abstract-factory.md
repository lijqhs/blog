---
title: Abstract Factory
slug: Abstract Factory
author: aaron
date: 2023-05-20T10:00:01
tags: ["python", "design pattern"]
---


The Abstract Factory pattern is a creational design pattern that provides an interface for creating families of related or dependent objects, without specifying their concrete classes. 

In this pattern, there is an abstract factory class that defines a set of abstract methods for creating related or dependent objects. Each concrete factory class that implements the abstract factory class provides its own implementation of these abstract methods, which creates specific families of related objects. The client code can then instantiate a specific concrete factory class and use its methods to create related objects without knowing their specific implementation details.

The main advantage of the Abstract Factory pattern is that it helps to decouple the client code from the specific classes of the objects it creates. This makes the code more flexible and easier to maintain, as it allows new families of objects to be added or existing ones to be modified without affecting the rest of the code. 

Here are the main components of the Abstract Factory pattern:

- **Abstract Factory:** This is an abstract base class that defines a set of abstract methods for creating related objects. These methods are implemented by the concrete factory classes. 

- **Concrete Factory:** This is a concrete class that implements the abstract factory class and provides its own implementation of the abstract methods. Each concrete factory class creates a specific family of related objects.

- **Abstract Product:** This is an abstract base class that defines a set of abstract methods for the objects that the factory creates. These methods are implemented by the concrete product classes.

- **Concrete Product:** These are concrete classes that implement the abstract product class and provide their own implementation of the abstract methods. Each concrete product class corresponds to a specific object created by the factory.

Here's an example scenario where the Abstract Factory pattern might be used:

Suppose you are developing a game that can be played on different platforms, such as Windows, macOS, and Linux. Each platform has its own set of graphics and sound assets that need to be loaded into the game. Using the Abstract Factory pattern, you can create an abstract factory class called `AssetFactory` that defines abstract methods for creating related graphics and sound assets. You can then create concrete factory classes such as `WindowsAssetFactory`, `MacOSAssetFactory`, and `LinuxAssetFactory`, each of which provides its own implementation of the `AssetFactory` methods to create graphics and sound assets that are appropriate for its platform. The client code can then create an instance of a specific concrete factory class and use its methods to load the appropriate assets without knowing their specific implementation details.

## Example

```python
from abc import ABC, abstractmethod

class Button(ABC):
    @abstractmethod
    def paint(self):
        pass

class WindowsButton(Button):
    def paint(self):
        return "Windows style button"

class MacOSButton(Button):
    def paint(self):
        return "MacOS style button"

class Checkbox(ABC):
    @abstractmethod
    def paint(self):
        pass

class WindowsCheckbox(Checkbox):
    def paint(self):
        return "Windows style checkbox"

class MacOSCheckbox(Checkbox):
    def paint(self):
        return "MacOS style checkbox"

class GUIFactory(ABC):
    @abstractmethod
    def create_button(self):
        pass

    @abstractmethod
    def create_checkbox(self):
        pass

class WindowsFactory(GUIFactory):
    def create_button(self):
        return WindowsButton()

    def create_checkbox(self):
        return WindowsCheckbox()

class MacOSFactory(GUIFactory):
    def create_button(self):
        return MacOSButton()

    def create_checkbox(self):
        return MacOSCheckbox()

# Usage
def create_gui(factory):
    button = factory.create_button()
    checkbox = factory.create_checkbox()
    print(button.paint())
    print(checkbox.paint())

windows_factory = WindowsFactory()
macos_factory = MacOSFactory()

create_gui(windows_factory)  # This will print "Windows style button" and "Windows style checkbox"
create_gui(macos_factory)    # This will print "MacOS style button" and "MacOS style checkbox"
```

In this example, we have an abstract base class `Button` and its subclasses `WindowsButton` and `MacOSButton`. We also have an abstract base class `Checkbox` and its subclasses `WindowsCheckbox` and `MacOSCheckbox`. Each subclass implements a `paint()` method that returns a string representing the appearance of the button or checkbox in their respective operating systems.

We also have an abstract factory class `GUIFactory` that defines two abstract methods `create_button()` and `create_checkbox()`. The concrete `WindowsFactory` and `MacOSFactory` classes implement these methods to create `Button` and `Checkbox` objects that are appropriate for their respective operating systems.

To use the Abstract Factory pattern, you can pass an instance of a concrete factory class to a function that knows how to create a GUI using the objects created by the factory. In this example, we pass instances of `WindowsFactory` and `MacOSFactory` to the `create_gui()` function, which creates a `Button` and a `Checkbox` object using the factory and calls their `paint()` methods to display their appearance.

By using the Abstract Factory pattern, we can create a GUI that is appropriate for the operating system without having to know the specific implementation details of each `Button` and `Checkbox` subclass. This allows us to create objects in a flexible and extensible way, and to decouple the client code from the specific classes of those objects.


## Factory Method vs. Abstract Factory

The Factory Method and Abstract Factory design patterns are creational patterns that help to create objects in a flexible and reusable way. 

The Factory Method pattern provides an interface for creating objects, but allows subclasses to decide which class to instantiate. This pattern is useful when you have a class that cannot anticipate the type of objects it needs to create, or when you want to delegate the responsibility of object creation to a subclass. 

The Abstract Factory pattern provides an interface for creating families of related or dependent objects, without specifying their concrete classes. This pattern is useful when you want to create a set of related objects that work together in a coherent way, but you want to decouple the client code from the specific classes of those objects. 

Here are some more specific purposes and benefits of using these patterns:

- **Encapsulation of object creation logic:** The Factory Method and Abstract Factory patterns encapsulate the details of object creation in a separate class or method, which helps to keep the client code simple and focused on its main responsibilities.

- **Flexibility and extensibility:** By using these patterns, you can easily add new types of objects or modify the way objects are created, without affecting the rest of the code. This makes your code more flexible and extensible, and can help to reduce maintenance costs over time.

- **Separation of concerns:** The Factory Method and Abstract Factory patterns separate the concerns of object creation from the rest of the code, which can make your code more modular, testable, and maintainable.

- **Polymorphism and abstraction:** By using these patterns, you can create objects in a polymorphic and abstract way, which makes your code more general and reusable. This can help to improve the overall design of your code and reduce code duplication.

- **Encourages best practices:** Using these patterns encourages the use of best practices such as dependency inversion, loose coupling, and single responsibility, which can lead to cleaner and better organized code.

Overall, the Factory Method and Abstract Factory design patterns are useful tools for managing object creation in a flexible and reusable way, and can help to improve the design and maintainability of your code.

## Reference

- https://stackoverflow.com/questions/5739611/what-are-the-differences-between-abstract-factory-and-factory-design-patterns
