---
title: Flyweight
slug: Flyweight
author: aaron
date: 2023-05-20T10:10:05
tags: ["python", "design pattern"]
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

- You can implement shared leaf nodes of the **Composite** tree as **Flyweights** to save some RAM.

- **Flyweight** shows how to make lots of little objects, whereas **Facade** shows how to make a single object that represents an entire subsystem.

- **Flyweight** would resemble **Singleton** if you somehow managed to reduce all shared states of the objects to just one flyweight object. But there are two fundamental differences between these patterns:
  - There should be only one Singleton instance, whereas a Flyweight class can have multiple instances with different intrinsic states.
  - The Singleton object can be mutable. Flyweight objects are immutable.
