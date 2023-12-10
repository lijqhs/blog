---
title: Name Mangling
slug: name-mangling
author: aaron
date: 2023-05-10
tags: ["python", "name mangling"]
---


Name mangling is a feature in Python that is used to avoid naming conflicts in class hierarchies by adding a prefix to the name of a class member that starts with two underscores, but does not end with more than one underscore.

When a member name is prefixed with two underscores, Python automatically rewrites the name in a way that makes it harder to access the member from outside the class. Specifically, it adds the class name as a prefix with an underscore, followed by the original member name.

For example, if a class `Person` has a private member named `__name`, Python will rewrite the name as `_Person__name`. This makes it harder to accidentally override the member from outside the class, and also makes it harder to access the member from outside the class, since the actual name of the member is different.

Here's an example of name mangling in action:

```python
class Person:
    def __init__(self, name):
        self.__name = name

class Employee(Person):
    def __init__(self, name, employee_id):
        super().__init__(name)
        self.employee_id = employee_id

    def get_name(self):
        return self.__name

employee = Employee('Alice', 123)
print(employee._Person__name)   # Output: Alice
```

In this example, the `Person` class has a private member named `__name`. When the `Employee` class inherits from `Person`, the private member is automatically mangled to `_Person__name`. When we create an `Employee` object and call the `get_name` method, the private member is accessed correctly using the `__name` name. However, when we try to access the member directly from outside the class using the mangled name `_Person__name`, we can access it, but it is generally considered bad practice to do so.

It is important to note that name mangling is not a security feature, and it does not prevent access to the member from outside the class. It is simply a way to avoid naming conflicts and provide a level of protection against accidental name collisions. In general, Python follows the philosophy of "we're all consenting adults here," which means that developers are trusted to respect the conventions of naming and access control.
