---
title: Python OOPs
permalink: /docs/pyoops-1/
---

## Object Oriented Python

Python may be used as a simple scripting language but it is a fully object oriented programming language, but as with every language it has its own approach to how it implements classes and other OOP features.  

Note : Python will happily let you put everything in a single file. I recommend you do not do this and stick with giving each class its own file and importing it where you need it. It makes it much easier to understand and maintain your code.  

## Class Definition

```python
class Dog:
  pass
```

Classes are defined using the `class` keyword and given a name. In Python class names should be in CamelCase.  The above code defines a class called `Dog` that has no methods and no member variables. The keyword `pass` does nothing, it simply allows us to write code with gaps in where gaps are not allowed.  

## Class Constructors

For most of the classes we create we will want to have constructors. In Python we create a constructor as shown below.  

```python
class Dog:
  def __init__(self, name, age):
    self.name = name
    self.age = age
```

We use `def` to define a function as usual but here the reserved function name `__init__` is used. `__init__` is the constructor function name in Python.  

The parameters are indicated after the `__init__`, in this case they are `self`, `name`, and `age`. `name` and `age` are normal parameters but `self` is special. `self` refers to the object itself. `self` is not actually passed as a parameter when an object of the class is created, it is handled by Python. The other parameters are used as normal. To create an object of the class we would do something like :  

```python
miles = Dog("Miles",4)
patch = Dog("Patch",1)
```

Unlike Java you cannot have multiple constructors. There are ways of doing this we will come to later.  

## Attributes

### Class Attributes

In Python member variables are called *attributes*. They are added to the class definition as normal (for Python variables).  

```python
class Dog:
  species = "Canis familiaris"
  def __init__(self, name, age):
    self.name = name
    self.age = age
```

Attributes can be access using `.` and the object name.  

```python
miles = Dog("Miles",4)
print(miles.name, miles.age, miles.species)
miles.age = 5
```

### Instance Attributes

Python classes have two different types of attributes. *Instance attributes* are attributes that must be provided when an object is created. These are the attributes from the `__init__` function. *Class attributes* are defined as part of the class and are set to defaults.  

## Instance Methods

Instance methods are functions that are defined within a class. Just like `__init__` an instance method's first parameter is always `self`. Always, even if it has no other parameters.  

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

Here we have added to instance methods.
1. `description()` takes no parameters and returns a description of the dog.
2. `speak()` takes a single parameter string containing the sound the dog makes (at that moment)

|Both methods use `f"some text"` in their return statements. `f""` is the format string function. It is used to build up a string from text and variables. The variables are place in {} curly brackets to indicate their placement. For more information of f"" see [https://realpython.com/python-f-strings/](https://realpython.com/python-f-strings/).  |

Methods are called as you'd expect.  

```python
miles = Dog("Miles",4)
print(miles.description())
print(miles.speak("Woof, Woof"))
```

### __str__ Method

Python provides for a number of methods like `__init__`. The `__str__` method allows you to "print" an object of the class and get a description.  

```python
class Dog:
  # Leave other parts of Dog class as-is

  def __str__(self):
    return f"{self.name} is {self.age} years old"
```

```python
miles = Dog("Miles",4)
print(miles)
```

Methods like `__init__` and `__str__` are known as **dunder methods** because they begin and end with double underscores. See here for more info on [dunder methods](https://medium.com/python-features/magic-methods-demystified-3c9e93144bf7)  

## Deleting Objects

Objects can be deleted with `del object`. Be careful though, there is no easy way to test if an object exists before you try to use it. 
## Inheritance

Inheritance is the process by which one class takes on the attributes and methods of another. Newly formed classes are called child classes, and the classes that child classes are derived from are called parent classes. Python, being an object oriented language lets us create a class that inherits from another class.  

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

```python
class JackRusselTerrier(Dog):
  def speak(self, sound="Arf"):
    return f"{self.name} says {sound}"

class Bulldog(Dog):
  def speak(self, sound="Gruff"):
    return f"{self.name} says {sound}"
```

Here we create a child class of `Dog` called `JackRusselTerrier` and override the speak method.  


### type() and isinstance()

Python provides 
* `type()` a method that will return the class an object belongs to
* `isinstance()` a method that will check to see if an object is an instance of a class. 

```python
bobby = JackRusselTerrier("Bobby",1)

print(type(bobby)))
print(isinstance(bobby,Dog))
print(isinstance(bobby,Bulldog))
print(isinstance(bobby,JackRusselTerrier))
```

## Encapsulation

We can restrict access to methods and attributes to prevent them from direct modification. We can make attributes `private` by prefixing them with and underscore `_` or double underscore `__`.  

```python
class Computer:

    def __init__(self):
        self.__maxprice = 900

    def sell(self):
        print("Selling Price: {}".format(self.__maxprice))

    def setMaxPrice(self, price):
        self.__maxprice = price

c = Computer()
c.sell()

# change the price
c.__maxprice = 1000
c.sell()

# using setter function
c.setMaxPrice(1000)
c.sell()
```

Output

```console
Selling Price: 900
Selling Price: 900
Selling Price: 1000
```

The line `c.__maxprice = 1000` does not change the value because it is `private` and can only be changed within the class.  

#### Exercise 1 

1. Log in to repl.it
2. Go to [https://repl.it/@andyguest/pyFirstClass](https://repl.it/@andyguest/pyFirstClass)
3. Click on the `fork` button at the top of the window to make a copy of the code in your own repls
4. Click on the three lines at the top left of the window and then `My Repls` in the pop out menu
5. Open the `pyFirstClass` repl from your area
6. The file `Dog.py` contains the Dog classes.
7. Work your way through the tasks in the code - they are in the comments

