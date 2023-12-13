---
title: Namedtuple
slug: namedtuple
author: aaron
date: 2023-04-11
tags: ["python", "namedtuple"]
---


The `namedtuple` function is a factory function from the `collections` module in Python that creates a new class-like object that behaves like a tuple, but with named fields. Here are some cases where you might consider using `namedtuple`:

1. Improved readability: If you have a collection of records or objects that have a fixed set of attributes, using a `namedtuple` can make your code more readable by giving names to the fields instead of relying on integer indices.

2. Concise code: `namedtuple` allows you to create simple classes without defining a class explicitly. This can make your code more concise and less verbose.

3. Immutable data: `namedtuple` instances are immutable, which means that once you create an instance, you cannot modify its fields. This can be useful when you want to ensure that your data remains constant throughout your program and that no unexpected changes can occur.

4. Interoperability with tuple-based APIs: Many Python modules and APIs expect tuples as input or return values. By using `namedtuple`, you can create objects that behave like tuples but also have named fields, making it easier to work with these APIs.

5. Memory efficiency: `namedtuple` instances are more memory-efficient than regular objects because they are implemented as tuples. This can be beneficial if you need to create many instances of a class-like object and want to minimize the memory footprint of your program.

### Examples

Here are some examples of situations where `namedtuple` can be useful:

1. Defining a data structure: If you need to represent a collection of related data, such as a point in a 2D space, a date or time, or a person's contact information, `namedtuple` can provide a lightweight and convenient way to define a data structure.

```python
from collections import namedtuple

# Define a Point namedtuple with x and y fields
Point = namedtuple('Point', ['x', 'y'])

# Create a new Point object
p = Point(1, 2)

# Access the x and y fields using named attributes
print(p.x, p.y)  # Output: 1 2
```

2. Returning multiple values from a function: If a function needs to return multiple values, `namedtuple` can be a cleaner and more readable alternative to using an ordinary tuple.

```python
from collections import namedtuple

# Define a Result namedtuple with success and message fields
Result = namedtuple('Result', ['success', 'message'])

def process_data(data):
    if validate_data(data):
        return Result(True, "Data is valid.")
    else:
        return Result(False, "Data is invalid.")
        
result = process_data(my_data)

if result.success:
    print("Success:", result.message)
else:
    print("Error:", result.message)
```

3. Subclassing: `namedtuple` can be subclassed to add custom methods and additional attributes, while still retaining the lightweight and efficient tuple-like behavior.

```python
from collections import namedtuple

# Define a Circle namedtuple with x, y, and radius fields
Circle = namedtuple('Circle', ['x', 'y', 'radius'])

class CirclePlus(Circle):
    def area(self):
        return 3.14 * self.radius ** 2

c = CirclePlus(0, 0, 5)
print(c.area())  # Output: 78.5
```

Overall, `namedtuple` can be useful in any situation where a simple, lightweight, and readable data structure is needed.

## When not to use `namedtuple`

However, there are also cases where `namedtuple` might not be appropriate. For example, if you need to add methods or properties to your class-like object, or if you need to customize the behavior of your object beyond what `namedtuple` provides, it may be better to define a regular class instead. Additionally, if you need to modify the fields of your object regularly, you should use a mutable object like a `dict` or a custom class instead of a `namedtuple`.

Here's an example where a regular class would be more appropriate than a `namedtuple`:

Let's say you are working on a project that involves creating a representation of a bank account. Each bank account has a unique account number, a balance, and a list of transactions. You might be tempted to use a `namedtuple` to represent a bank account like this:

```python
from collections import namedtuple

BankAccount = namedtuple('BankAccount', ['account_number', 'balance', 'transactions'])

account1 = BankAccount('123456', 1000, [('deposit', 500), ('withdrawal', 200)])
```

This code creates a `namedtuple` called `BankAccount` with three fields: `account_number`, `balance`, and `transactions`. You can create instances of this `namedtuple` by passing in values for each of the fields.

However, using a regular class would be more appropriate in this case, for the following reasons:

1. Encapsulation: With a class, you can encapsulate the behavior of a bank account, and make sure that users of the class interact with it in a safe and consistent way. For example, you might want to ensure that the balance of the account is never negative, or that transactions are added in a specific way.

2. Flexibility: With a class, you can easily add new methods or properties to the bank account object as needed. For example, you might want to add a method to calculate the interest on the account, or a property to check if the account is overdrawn.

3. Maintainability: A class-based implementation will be easier to maintain in the long run, especially if the requirements of the bank account object change over time. With a class, you can easily modify the behavior of the object without affecting the rest of your codebase.

Here's an example of how you might implement the `BankAccount` class:

```python
class BankAccount:
    def __init__(self, account_number, balance, transactions=None):
        self.account_number = account_number
        self._balance = balance
        self._transactions = transactions or []
        
    @property
    def balance(self):
        return self._balance
    
    def deposit(self, amount):
        self._balance += amount
        self._transactions.append(('deposit', amount))
        
    def withdraw(self, amount):
        if self._balance - amount < 0:
            raise ValueError("Insufficient funds")
        self._balance -= amount
        self._transactions.append(('withdrawal', amount))
        
    def add_transaction(self, transaction):
        self._transactions.append(transaction)
```

This implementation uses a regular class to define the `BankAccount` object. The class has methods to deposit and withdraw funds, and a property to get the current balance of the account. It also has an `add_transaction` method to add new transactions to the account.

Using a class-based implementation like this can make your code more maintainable, flexible, and encapsulated.
