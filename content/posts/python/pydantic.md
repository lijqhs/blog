---
title: Pydantic Library
slug: Pydantic
author: aaron
date: 2023-10-21
tags: ["python", "pydantic"]
categories: ["Python Tips"]
---

## Pydantic Library

Pydantic v2 is a powerful data validation and serialization library for Python. It leverages Python's type hints to provide runtime data validation, making your code more robust and easier to maintain. 

### Installation

To install Pydantic, use pip:

```bash
pip install pydantic
```

For email validation, you can install the optional `email-validator` dependency:

```bash
pip install pydantic[email]
```

### Basic Concepts

#### Models

Pydantic models are classes that inherit from `BaseModel` and define fields with type annotations. These models are used to validate and serialize data.

```python
from pydantic import BaseModel, EmailStr
from datetime import datetime

class User(BaseModel):
    id: int
    name: str = 'John Doe'
    email: EmailStr
    age: int
    signup_ts: datetime | None
```

#### Validation

Pydantic automatically validates data when you instantiate a model. If the data is invalid, a `ValidationError` is raised.

```python
from pydantic import BaseModel, ValidationError
from datetime import datetime

class User(BaseModel):
    id: int
    name: str
    signup_ts: datetime | None

data = {
    'id': '123',
    'name': 'Alice',
    'signup_ts': '2023-07-20 12:22'
}

try:
    user = User(**data)
    print(user)
except ValidationError as e:
    print(e)
```

### Validators

Validators in Pydantic allow you to add custom validation logic to your models. They can be defined using the `@field_validator` and `@model_validator` decorators.

#### Field Validators

Field validators are used to validate specific fields. They are defined using the `@field_validator` decorator and should be class methods for better type checking.

```python
from pydantic import BaseModel, field_validator, EmailStr

class User(BaseModel):
    name: str
    email: EmailStr

    @field_validator('name')
    @classmethod
    def name_must_contain_space(cls, v):
        if ' ' not in v:
            raise ValueError('must contain a space')
        return v.title()

    @field_validator('email')
    @classmethod
    def email_must_be_valid(cls, v):
        if '@' not in v:
            raise ValueError('must be a valid email')
        return v
```

#### Model Validators

Model validators are used to validate the entire model. They are defined using the `@model_validator` decorator.

```python
from pydantic import BaseModel, model_validator

class User(BaseModel):
    password1: str
    password2: str

    @model_validator
    @classmethod
    def check_passwords_match(cls, values):
        if values['password1'] != values['password2']:
            raise ValueError('passwords do not match')
        return values
```

### Examples

#### Simple Model

```python
from pydantic import BaseModel, EmailStr

class Employee(BaseModel):
    name: str
    age: int
    email: EmailStr
    department: str
    employee_id: str

employee = Employee(
    name="John Doe",
    age=30,
    email="john.doe@example.com",
    department="Engineering",
    employee_id="123456"
)
print(employee)
```

#### Custom Validators

You can define custom validators using the `@field_validator` decorator.

```python
from pydantic import BaseModel, field_validator, EmailStr

class Employee(BaseModel):
    name: str
    age: int
    email: EmailStr
    department: str
    employee_id: str

    @field_validator('employee_id')
    @classmethod
    def validate_employee_id(cls, v):
        if not v.isalnum() or len(v) != 6:
            raise ValueError('Employee ID must be exactly 6 alphanumeric characters')
        return v

try:
    employee = Employee(
        name="John Doe",
        age=30,
        email="john.doe@example.com",
        department="Engineering",
        employee_id="12345"  # Invalid ID
    )
except ValidationError as e:
    print(e)
```

### Best Practices

1. **Use Type Hints**: Leverage Python's type hints for all fields to enable automatic validation.
2. **Custom Validators**: Implement custom validators for complex validation logic.
3. **Strict Mode**: Use `strict=True` mode to avoid automatic type coercion and ensure data integrity.
4. **Data Serialization**: Utilize Pydantic's serialization methods like `model_dump` for converting models to dictionaries or JSON.

### Common Use Scenarios

- **API Development**: Pydantic is extensively used in frameworks like FastAPI for request and response validation.
- **Data Parsing**: Pydantic can parse and validate data from various sources like JSON files or API responses.
- **Configuration Management**: Use Pydantic models to validate and manage application configurations.

### Successful Applications

Pydantic is widely adopted in the Python ecosystem, with notable usage in:

- **FastAPI**: A modern web framework for building APIs with Python 3.6+ based on standard Python type hints.
- **Hugging Face**: A leading NLP library that uses Pydantic for model configuration.
- **SQLModel**: A library for interacting with SQL databases using Python type hints.

For more detailed information, refer to the [Pydantic documentation](https://docs.pydantic.dev/latest/).
