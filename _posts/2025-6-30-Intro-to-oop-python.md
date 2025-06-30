---
title: Intro To Object Oriented Programming.
tags: [oop, python]
layout: post
---

## Summary
- Simple definition
- The four tenants of OOP
- How Do You Define a Class in Python?
    - Classes VS Instances
    - Class Definition
- How Do You Instantiate a Class in Python?
    - Instance Methods.
- How Do You Inherit From Another Class in Python?

---
- Programming paradigm, that makes use of object, any object could have ``properties`` and ``behaviors``

---
## The four tenants of OOP
- **Encapsulation** (Keeps things together and protected): allow you to put data (attributes) and behaviors (methods) within one class, by defining attributes to allow access to attributes and its modification, to make the code modular and secure, and no loose data integrity.
- **Inheritance**: Allowing ``subclasses`` to inherit from a ``parent class``  which make the code reusable and prevent repetition.
- **Abstraction**: exposing only the essential functionality of an object, allowing developers to focus only on what the object does rather than how it achieves its functionality.
- **Polymorphism**: If two different objects have a method with the **same name** (even if the **implementation is different**), you can use that method **without worrying about the object's class**. As long as the method exists, Python will run the correct version based on the object's type.

Polymorphism example:
```python
class Dog:
    def speak(self):
        return "Woof!"

class Cat:
    def speak(self):
        return "Meow!"

def make_sound(animal):
    print(animal.speak())  # We don’t care if it’s a Dog or a Cat

make_sound(Dog())  # Woof!
make_sound(Cat())  # Meow!

```

## How Do You Define a Class in Python?
- Using the ``class`` keyword followed by a name and colon.
- then ``__init__()`` to declare which attributes each method should have.
```python
class Employee:
    def __init__(self, name, age):
        self.name =  name
        self.age = age
```

### Classes VS Instances:
- **Class** are blueprints and they don t contain data, they allow you to create user-defined data structures, and ``methods`` which define the behavior.
- **Instances** in the other hand are objects that are built from a class, and they contain real data.

### Class Definition:
- We begin by using ``class`` keyword then a name followed by colon, any code indented bellow is considered the body of the class.
```python
class Dog:
    pass
```
- We should now add properties to Dog, like name and age.
- We use ``__init__()`` method which initializes the state of the object by assigning the values of the properties .
- We can give ``__init__()`` any number of parameters but the first one will always be ``self`` when you create a new instances python automatically passes the instance to the ``self`` parameter.
```python
class Dog:
    def __init__(self, name, age):
        self.name = name
        self.age = age
```
- attributes in ``__init__()`` are called instance attributes each instance has its own name and age.
- class attributes have the same value across all the instances.
```python
class Dog:
	# class attibute
    species = "Canis familiaris"

    def __init__(self, name, age):
        self.name = name
        self.age = age
```
 - class attributes should have an initial value, and once an instance is created python automatically creates and assign class attributes to their initial values.

## How Do You Instantiate a Class in Python?
- you can do that by typing the name of the class followed by parenthesis.
```python
>>> class Dog:
...     pass
...
>>> Dog()
<__main__.Dog object at 0x106702d30>
```
- 0x106702d30 is where the instance is located in memory, each instance have its own memory address.
```python
>>> class Dog:
...     species = "Canis familiaris"
...     def __init__(self, name, age):
...         self.name = name
...         self.age = age
...
```
- We instantiate by doing the following
```python
>>> miles = Dog("Miles", 4)
>>> buddy = Dog("Buddy", 9)
```
- Note that not providing the two arguments will result in a ``TypeError``
- You can access instances attributes the following:
```python
>>> miles.name
'Miles'
>>> miles.age
4

>>> buddy.name
'Buddy'
>>> buddy.age
9
```
- same goes for class attributes
```python
>>> buddy.species
'Canis familiaris'
```
- Changing the values of attributes dynamically.
```python
>>> buddy.age = 10
>>> buddy.age
10

>>> miles.species = "Felis silvestris"
>>> miles.species
'Felis silvestris'
```
- so we can conclude here that custom objects are mutable by default.

### Instance Methods:
- they are methods defined inside a class and can only call on an instance of that class, and they take ``self`` as their first parameter.
```python
class Dog:
    species = "Canis familiaris"

    def __init__(self, name, age):
        self.name = name
        self.age = age

    # Instance method
    def description(self):
        return f"{self.name} is {self.age} years old"

    # Another instance method
    def speak(self, sound):
        return f"{self.name} says {sound}"
```
1. first instance method is ``description()`` and it returns a string containing information about the dog
2. second instance method is ``speak()`` which has a sound parameter and returns the name and the dog sound.
```python
>>> miles = Dog("Miles", 4)

>>> miles.description()
'Miles is 4 years old'

>>> miles.speak("Woof Woof")
'Miles says Woof Woof'

>>> miles.speak("Bow Wow")
'Miles says Bow Wow'
```
- using description to return that kind of string is not really a ***pythonic*** way of doing things,
what you wanna do instead is using a special instance method called ``__str__()``
```python
class Dog:
    # ...

    def __str__(self):
        return f"{self.name} is {self.age} years old"
```

```python
>>> miles = Dog("Miles", 4)
>>> print(miles)
'Miles is 4 years old'
```

- ``__str__()`` and ``__init__()`` are called **dunder methods**.

## How Do You Inherit From Another Class in Python:
- Inheritance is when a class inherits attributes and methods from another class, it's a **parent/child** relationship.
```python
class Parent:
    hair_color = "brown"

class Child(Parent):
    pass
```
- In this example Child class inherits from parent, so Child.hair_color is automatically brown.
- Child classes can override or extend the attributes and methods of parent classes
```python
class Parent:
    hair_color = "brown"

class Child(Parent):
    hair_color = "purple"
```
- What if we wanna expend not just override.
```python
class Parent:
    speaks = ["English"]

class Child(Parent):
    def __init__(self):
        super().__init__()
        self.speaks.append("German")
```
- To check if something is an instance of a class we use ``isisttance(object, class)``

***Conculsion***:
- Define a **class**, which is a sort of blueprint for an object
- Instantiate a class to create an **object**
- Use **attributes** and **methods** to define the **properties** and **behaviors** of an object
- Use **inheritance** to create **child classes** from a **parent class**
- Reference a method on a parent class using **`super()`**
- Check if an object inherits from another class using **`isinstance()`**
