---
title: Flyweight Pattern
slug: Flyweight Pattern
author: aaron
date: 2023-05-20T10:10:05
series: ["Design Patterns"]
# tags: ["flyweight pattern", "proxy pattern", "composite pattern", "factory pattern", "decorator pattern", "iterator pattern"]
---


The Flyweight pattern is a software design pattern that is used to minimize memory usage by sharing data between multiple objects. It is a structural pattern that is used to manage large numbers of small, similar objects in an efficient way.

The main idea behind the Flyweight pattern is to share common parts of objects between multiple instances, rather than creating new instances for each object. This can help to reduce memory usage and improve the performance of your code.

## Example

Let's say you are building a text editor application that allows users to create and edit documents. Each document may contain many characters, and each character has its own attributes such as font size, font color, and style.

One way to implement this would be to create a separate object for each character in the document, which would quickly become very memory-intensive and slow. Instead, you could use the Flyweight pattern to share common character attributes between multiple characters, reducing the number of objects needed and improving the performance of the application.

Here's an example implementation:

```python
class Character:
    def __init__(self, char, font_size, font_color, font_style):
        self.char = char
        self.font_size = font_size
        self.font_color = font_color
        self.font_style = font_style

    def print(self):
        print(f"Character '{self.char}' with font size {self.font_size}, color {self.font_color} and style {self.font_style}")

class CharacterFactory:
    _characters = {}

    def get_character(self, char, font_size, font_color, font_style):
        key = f"{char}{font_size}{font_color}{font_style}"
        if key not in self._characters:
            self._characters[key] = Character(char, font_size, font_color, font_style)
        return self._characters[key]

class Document:
    def __init__(self):
        self._characters = []

    def add_character(self, char, font_size, font_color, font_style):
        factory = CharacterFactory()
        character = factory.get_character(char, font_size, font_color, font_style)
        self._characters.append(character)

    def print(self):
        for character in self._characters:
            character.print()

# Usage
document = Document()
document.add_character('H', 12, 'black', 'bold')
document.add_character('e', 12, 'black', 'bold')
document.add_character('l', 12, 'black', 'bold')
document.add_character('l', 12, 'black', 'bold')
document.add_character('o', 12, 'black', 'bold')
document.add_character('!', 12, 'black', 'bold')
document.add_character(' ', 12, 'black', 'normal')
document.add_character('W', 12, 'red', 'bold')
document.add_character('o', 12, 'red', 'bold')
document.add_character('r', 12, 'red', 'bold')
document.add_character('l', 12, 'red', 'bold')
document.add_character('d', 12, 'red', 'bold')
document.add_character('!', 12, 'red', 'bold')
document.print()
```

In this example, we have a `Character` class that represents a character in the document, and a `CharacterFactory` class that manages the creation and sharing of `Character` objects.

The `Document` class represents a document, and has a method `add_character` that takes character attributes and uses the `CharacterFactory` to create or retrieve a shared `Character` object for that set of attributes.

When we create a `Document` object and add multiple characters with the same attributes, the `CharacterFactory` returns the same shared `Character` object, reducing the memory usage of the application. When we call the `print` method of the `Document` object, it prints out the characters with their respective attributes.

This example demonstrates how the Flyweight pattern can be used to efficiently manage large numbers of similar objects with shared attributes, such as characters in a text editor.

## Relations with Other Patterns

The Flyweight pattern is a structural design pattern that aims to optimize memory usage by sharing common data across multiple objects. It achieves this by separating intrinsic (shared) state from extrinsic (unique) state, with the intrinsic state being shared among multiple objects.

The Flyweight pattern can be related to other design patterns in the following ways:

1. Composite Pattern: The Flyweight pattern can be used in conjunction with the Composite pattern to optimize memory usage in a hierarchical structure. The Flyweight objects can represent shared properties or data that are common to multiple elements in the composite structure, reducing memory consumption.

2. Factory Pattern: The Factory pattern can be used with the Flyweight pattern to manage the creation and retrieval of Flyweight objects. The Factory pattern encapsulates the creation logic and ensures that Flyweight objects are shared and reused appropriately.

3. Proxy Pattern: The Proxy pattern can be combined with the Flyweight pattern to control access to shared Flyweight objects. The Proxy acts as a wrapper around the Flyweight objects, providing additional functionality such as access control or lazy loading.

4. Decorator Pattern: The Flyweight pattern can work in conjunction with the Decorator pattern to add additional behavior or responsibilities to Flyweight objects. The Decorator pattern allows you to dynamically wrap Flyweight objects with decorators, extending their functionality without affecting the shared intrinsic state.

5. Iterator Pattern: The Flyweight pattern can be used with the Iterator pattern to iterate over a collection of Flyweight objects. The Iterator pattern provides a way to traverse and access the shared Flyweight objects without exposing the underlying representation or structure.

It's important to note that the Flyweight pattern is primarily focused on memory optimization by sharing common data, while the mentioned patterns serve different purposes. The choice of which patterns to use in conjunction with the Flyweight pattern depends on the specific requirements and constraints of the system being designed.