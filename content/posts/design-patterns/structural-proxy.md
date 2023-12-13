---
title: Proxy Pattern
slug: Proxy Pattern
author: aaron
date: 2023-05-20T10:10:06
series: ["Design Patterns"]
tags: ["proxy pattern", "adapter pattern", "singleton pattern", "flyweight pattern", "observer pattern"]
---


The Proxy pattern is a software design pattern that provides a surrogate or placeholder object to control access to another object. It is a structural pattern that allows you to create a class that represents the functionality of another class, while adding additional functionality such as access control, caching, or logging.

The main idea behind the Proxy pattern is to provide a level of indirection between the client and the real object, allowing you to control access to the real object and add additional functionality without modifying the real object's code.

## Example 1

The Proxy pattern is a software design pattern that provides a surrogate or placeholder object to control access to another object. It is a structural pattern that allows you to create a class that represents the functionality of another class, while adding additional functionality such as access control, caching, or logging.

The main idea behind the Proxy pattern is to provide a level of indirection between the client and the real object, allowing you to control access to the real object and add additional functionality without modifying the real object's code.

Here's an example of the Proxy pattern in Python:

```python
# Subject interface
class Subject:
    def request(self):
        pass

# Real subject class
class RealSubject(Subject):
    def request(self):
        print("RealSubject: Handling request.")

# Proxy class
class Proxy(Subject):
    def __init__(self, real_subject: RealSubject):
        self._real_subject = real_subject

    def request(self):
        if self.check_access():
            self._real_subject.request()
            self.log_access()

    def check_access(self):
        print("Proxy: Checking access prior to firing a real request.")
        return True

    def log_access(self):
        print("Proxy: Logging the time of request.")

# Client code
def client_code(subject: Subject):
    subject.request()

# Usage
real_subject = RealSubject()
proxy = Proxy(real_subject)
client_code(proxy)
```

In this example, we have a `Subject` interface that defines the common interface for both the `RealSubject` and `Proxy` classes. The `RealSubject` class represents the real object that the client wants to access, and the `Proxy` class represents the surrogate or placeholder object that controls access to the real object.

The `Proxy` class has a reference to the `RealSubject` object, and overrides the `request` method to add additional functionality such as access control and logging. The `check_access` method checks if the client has the necessary permissions to access the real object, and the `log_access` method logs the time of the request.

When we create a `RealSubject` object and a `Proxy` object that wraps it, and then pass the `Proxy` object to the `client_code` function, we get the output:

```
Proxy: Checking access prior to firing a real request.
RealSubject: Handling request.
Proxy: Logging the time of request.
```

As you can see, the `Proxy` class controls access to the real object, checks the client's permissions, and logs the time of the request. This allows you to add additional functionality to the real object without modifying its code.

## Example 2

Sure! Here's an example scenario where the Proxy pattern could be useful:

Let's say you are developing a web application that accesses a remote database. Accessing the remote database can be slow and expensive, so you want to implement a caching mechanism to improve performance. However, you don't want to modify the code of the application that accesses the database directly.

In this scenario, you could use the Proxy pattern to create a caching proxy that sits between the application and the remote database. The caching proxy would store the results of previous requests in memory, and would return the cached results instead of accessing the remote database if the requested data is available in the cache. This can help to improve the performance of the application by reducing the number of requests to the remote database.

Here's an example implementation of the Proxy pattern in Python for this scenario:

```python
# Subject interface
class Database:
    def query(self, query):
        pass

# Real subject class
class RemoteDatabase(Database):
    def query(self, query):
        print(f"RemoteDatabase: Executing query {query}")
        # Execute query on remote database and return results

# Proxy class with caching
class CachingProxy(Database):
    def __init__(self, remote_database: RemoteDatabase):
        self._remote_database = remote_database
        self._cache = {}

    def query(self, query):
        if query in self._cache:
            print(f"CachingProxy: Returning cached results for query {query}")
            return self._cache[query]
        else:
            print(f"CachingProxy: Executing query {query} and caching results")
            result = self._remote_database.query(query)
            self._cache[query] = result
            return result

# Client code
def client_code(database: Database, query):
    database.query(query)
    database.query(query)

# Usage
remote_database = RemoteDatabase()
caching_proxy = CachingProxy(remote_database)
client_code(caching_proxy, "SELECT * FROM customers")
```

In this example, we have a `Database` interface that defines the common interface for both the `RemoteDatabase` and `CachingProxy` classes. The `RemoteDatabase` class represents the real object that accesses the remote database, and the `CachingProxy` class represents the proxy object that adds caching functionality.

The `CachingProxy` class has a reference to the `RemoteDatabase` object, and overrides the `query` method to add caching functionality. The `query` method first checks if the requested data is available in the cache, and returns the cached results if it is. If the requested data is not in the cache, it retrieves the data from the remote database, caches the results, and returns the results.

When we create a `RemoteDatabase` object and a `CachingProxy` object that wraps it, and then pass the `CachingProxy` object to the `client_code` function with a query, we get the output:

```
CachingProxy: Executing query SELECT * FROM customers and caching results
RemoteDatabase: Executing query SELECT * FROM customers
CachingProxy: Returning cached results for query SELECT * FROM customers
```

As you can see, the `CachingProxy` class caches the results of the first query and returns the cached results for the second query, without accessing the remote database again. This helps to improve the performance of the application by reducing the number of requests to the remote database.

## Relations with Other Patterns

The Proxy pattern is a structural design pattern that provides a surrogate or placeholder for another object to control its access. It allows you to add an additional layer of indirection to control the interactions between clients and the real object. The Proxy pattern can be used for various purposes such as access control, caching, or lazy initialization.

The Proxy pattern can be related to other design patterns in the following ways:

1. Decorator Pattern: Both the Proxy pattern and the Decorator pattern involve wrapping an object with additional functionality. However, the intent of the Proxy pattern is to control access to the object, while the Decorator pattern is focused on adding new behavior or responsibilities to the object.

2. Adapter Pattern: The Proxy pattern and the Adapter pattern are similar in that they both act as intermediaries between clients and objects. However, the Adapter pattern is used to provide a different interface to an existing object, while the Proxy pattern controls access to an object.

3. Singleton Pattern: The Proxy pattern can use the Singleton pattern to ensure that there is only one instance of the Proxy object. This can be useful when you want to control access to a shared resource or manage the creation of the real object.

4. Flyweight Pattern: The Proxy pattern can work in conjunction with the Flyweight pattern to control access to shared Flyweight objects. The Proxy can act as a surrogate for the Flyweight object, providing additional functionality such as access control or lazy loading.

5. Observer Pattern: The Proxy pattern can be used with the Observer pattern to implement lazy initialization or delayed notification. The Proxy can act as a placeholder for the real object until it is actually needed, and the Observer pattern can be used to notify the Proxy when the real object becomes available.

These patterns can be used in combination or independently, depending on the specific requirements and constraints of the system being designed. The choice of which patterns to use depends on the problem at hand and the desired functionality and behavior.