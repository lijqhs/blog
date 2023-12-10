---
title: Builder
slug: Builder
author: aaron
date: 2023-05-20T10:00:02
tags: ["python", "design pattern"]
---


The Builder pattern is a creational design pattern that separates the construction of a complex object from its representation, allowing the same construction process to create different representations. It provides an interface for creating an object in a step-by-step manner, giving the developer more control over the construction process and allowing them to create complex objects in a more readable and maintainable way.

In the Builder pattern, there is a builder class that provides methods for setting each property of the object being constructed. The builder class can have multiple concrete implementations, each implementing the same interface but providing a different way to construct the object. Once the object is fully constructed, the builder returns the final object to the client.

The main advantage of the Builder pattern is that it allows the client code to create complex objects in a step-by-step manner, without having to know the specific implementation details of the object being constructed. It also allows the same construction process to create different representations of the object, giving the developer more flexibility and control over the construction process.

The Builder pattern is typically used in the following scenarios:

- When the object being constructed is complex and has many properties that need to be set in a specific order or with certain constraints.
- When the object's construction involves optional properties or properties with default values, allowing the developer to set only the necessary properties and leave the rest to default values.
- When the object being constructed needs to support multiple representations or configurations.

Here's an example scenario where the Builder pattern might be used:

Suppose you are developing a web application that allows users to create customized pizzas. Each pizza can have a variety of toppings, sauces, and crust types, and the final price of the pizza is based on the combination of these properties. Using the Builder pattern, you can create a `PizzaBuilder` class that provides methods for setting each property of the pizza, such as `setToppings()`, `setSauce()`, and `setCrust()`. The `PizzaBuilder` class can have multiple concrete implementations, each providing a different way to construct the pizza based on the user's preferences. Once the pizza is fully constructed, the `PizzaBuilder` returns the final pizza object to the client. This allows the client to create a customized pizza in a step-by-step manner, without having to know the specific implementation details of the pizza being constructed.
