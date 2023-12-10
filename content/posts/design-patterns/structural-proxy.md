---
title: Proxy
slug: Proxy
author: aaron
date: 2023-05-20T10:10:06
tags: ["python", "design pattern"]
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

- **Adapter** provides a different interface to the wrapped object, **Proxy** provides it with the same interface, and Decorator provides it with an enhanced interface.

- **Facade** is similar to **Proxy** in that both buffer a complex entity and initialize it on its own. Unlike Facade, Proxy has the same interface as its service object, which makes them interchangeable.

- **Decorator** and **Proxy** have similar structures, but very different intents. Both patterns are built on the composition principle, where one object is supposed to delegate some of the work to another. The difference is that a Proxy usually manages the life cycle of its service object on its own, whereas the composition of Decorators is always controlled by the client.
