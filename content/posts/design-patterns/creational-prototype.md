---
title: Prototype
slug: Prototype
author: aaron
date: 2023-05-20T10:00:03
tags: ["python", "design pattern"]
---


Design patterns in software engineering are reusable solutions to common problems that arise in software development. One such design pattern is the Prototype Design Pattern, which is used to create new objects by cloning existing objects. In this article, we will explore what the Prototype Design Pattern is, when to use it, examples, pros and cons, and related design patterns.

## What is the Prototype Design Pattern

The Prototype Design Pattern is a creational design pattern that allows the creation of new objects by copying existing objects. The existing object serves as a prototype, and the new object is created by cloning the prototype. This pattern is useful when creating objects is costly or complex, and the new objects have similar attributes to existing objects.

The Prototype Design Pattern defines an interface for cloning objects, which is implemented by concrete classes. The concrete classes create a clone of the prototype object and then modify it as required. This pattern allows the creation of new objects by copying existing objects, which is faster and less error-prone than creating new objects from scratch.

## When to use the Prototype Design Pattern

The Prototype Design Pattern can be used in the following scenarios:

- When creating objects is costly or complex
- When the new objects have similar attributes to existing objects
- When a system needs to be independent of how its products are created, composed, and represented
- When a system needs to be configured with objects at runtime

## Examples

Let'sconsider an example to understand the Prototype Design Pattern better. Suppose we have a prototype object, Car, which has various attributes such as color, model, engine type, etc. We want to create new cars with similar attributes as the prototype Car. In this case, we can use the Prototype Design Pattern to create new cars by cloning the prototype Car.

### Java example

```java
public abstract class Car implements Cloneable {
    protected String color;
    protected String model;
    protected String engineType;

    public abstract void drive();

    public Object clone() {
        Object clone = null;
        try {
            clone = super.clone();
        } catch (CloneNotSupportedException e) {
            e.printStackTrace();
        }
        return clone;
    }
}

public class Hatchback extends Car {
    public Hatchback() {
        this.color = "Red";
        this.model = "Honda Jazz";
        this.engineType = "Petrol";
    }

    @Override
    public void drive() {
        System.out.println("Driving a Hatchback car");
    }
}

public class Sedan extends Car {
    public Sedan() {
        this.color = "Blue";
        this.model = "Volkswagen Vento";
        this.engineType = "Diesel";
    }

    @Override
    public void drive() {
        System.out.println("Driving a Sedan car");
    }
}

public class CarFactory {
    private static Map<String, Car>carMap = new HashMap<>();

    static {
        carMap.put("Hatchback", new Hatchback());
        carMap.put("Sedan", new Sedan());
    }

    public static Car getCar(String carType) {
        return (Car) carMap.get(carType).clone();
    }
}
```

In the above code, we have a Car abstract class that implements the Cloneable interface. We have two concrete classes, Hatchback and Sedan, that extend the Car class and implement the drive() method. We also have a CarFactory class that has a HashMap of Car objects and a getCar() method that returns a cloned Car object based on the carType parameter passed.

### Python example

```python
import copy

class Car:
    def __init__(self, color, model, engine_type):
        self.color = color
        self.model = model
        self.engine_type = engine_type

    def drive(self):
        print(f"Driving a {self.color} {self.model} car with a {self.engine_type} engine")

    def clone(self):
        return copy.deepcopy(self)

class CarFactory:
    def __init__(self):
        self.car_map = {}

    def register_car(self, car_name, car):
        self.car_map[car_name] = car

    def unregister_car(self, car_name):
        del self.car_map[car_name]

    def get_car(self, car_name):
        return self.car_map[car_name].clone()

# Create a car factory
factory = CarFactory()

# Create a prototype car
prototype_car = Car("Red", "Honda Jazz", "Petrol")

# Register the prototype car with the factory
factory.register_car("Hatchback", prototype_car)

# Create a new car by cloning the prototype car
new_car = factory.get_car("Hatchback")

# Modify the new car's color
new_car.color = "Blue"

# Drive the prototype car and the new car
prototype_car.drive()
new_car.drive()
```

In this example, we define a `Car` class with a `clone` method thatreturns a deep copy of the object using the `copy` module. We also define a `CarFactory` class that keeps track of registered cars and can create new cars by cloning the registered prototypes.

We create a prototype car and register it with the factory. Then, we create a new car by cloning the prototype using the factory's `get_car` method. We modify the new car's color to "Blue" and then drive both the prototype car and the new car.

The output of running this code would be:

```
Driving a Red Honda Jazz car with a Petrol engine
Driving a Blue Honda Jazz car with a Petrol engine
```

As we can see, the prototype car and the new car have the same model and engine type, but the new car has a different color. This demonstrates the ability of the Prototype Design Pattern to create new objects with similar attributes to existing objects.

## Pros and Cons of the Prototype Design Pattern

Pros:
- Reduces the need for creating objects from scratch, which is faster and less error-prone
- Allows the creation of new objects with similar attributes to existing objects
- Improves performance by avoiding costly object creation
- Allows dynamic configuration of objects at runtime

Cons:
- Cloning objects can be complex and may require deep cloning to avoid shared references to mutable objects
- Requires implementing the Cloneable interface, which can be restrictive in some cases
- Can lead to excessive use of memory if many objects need to be cloned

## Related Design Patterns

The Prototype pattern is a creational design pattern that allows you to create new objects by cloning existing ones. Instead of creating objects from scratch, the Prototype pattern provides a way to create copies of an existing object and customize them as needed. This pattern is useful when creating new objects can be expensive or complex.

The Prototype pattern can be related to other design patterns in the following ways:

1. Abstract Factory Pattern: The Abstract Factory pattern and the Prototype pattern can be used together to create families of related objects. The Abstract Factory provides an interface for creating families of objects, while the Prototype pattern allows you to clone existing objects within those families.

2. Singleton Pattern: The Singleton pattern and the Prototype pattern are two different approaches to managing object creation. The Singleton pattern ensures that only one instance of a class exists, while the Prototype pattern allows you to create multiple instances of a class by cloning existing objects.

3. Builder Pattern: The Builder pattern and the Prototype pattern are both creational patterns, but they serve different purposes. The Builder pattern is used to construct complex objects step by step, while the Prototype pattern focuses on creating copies of existing objects.

4. Composite Pattern: The Prototype pattern can be used in conjunction with the Composite pattern to create a tree-like structure of objects. The Prototype pattern allows you to clone and customize objects, and the Composite pattern enables you to create a hierarchy of these objects.

5. Memento Pattern: The Memento pattern and the Prototype pattern can be used together to capture and restore the state of an object. The Prototype pattern allows you to create a clone of an object, which can then be stored as a Memento and later restored to its previous state.

It's important to note that the Prototype pattern emphasizes the creation of objects through cloning, while the mentioned patterns have different focuses and serve different purposes. The choice of which patterns to use in conjunction with the Prototype pattern depends on the specific requirements and constraints of the system being designed.