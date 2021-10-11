---
title: Python Basics
permalink: /docs/py-1/
---

## Running Python Code

Python applications are launched from the command line with `python filename.py`.  

Python acts like a scripting language. When you run a python file the code in the file executes from top to bottom.  

 <iframe height="400px" width="100%" src="https://replit.com/@andyguest/pyHelloWorld?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>  

This is the main body of the code. Functions and classes are defined above the main body of code (or in separate files) and are not execute automatically. They are only executed when called from the main body of the code.  

<iframe height="400px" width="100%" src="https://replit.com/@andyguest/pyFirstFunction?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>  

In Python files you will often find a main wrapper. It looks like this  

<iframe height="400px" width="100%" src="https://replit.com/@andyguest/pyMainWrapper?lite=true" scrolling="no" frameborder="no" allowtransparency="true" allowfullscreen="true" sandbox="allow-forms allow-pointer-lock allow-popups allow-same-origin allow-scripts allow-modals"></iframe>  

A function named `main()` is defined and the top level of code is written in there, just like a Java application. At the bottom of the file is an if statement  
```python
if __name__ == "__main__":
  main()
```
This if statement is the first part of the file that is run and will trigger the `main()`. It has two purposes, firstly it gives a main function which keeps the code sstructured nicely. Secondly when you build a project with multiple files you can include this in every file, then each file can be run independantly but `main()` only gets called for the file that is run.  

*A Python application is is launched with the command `python filename.py`. `__name__` is only set to `__main__` in the python file used to launch the application. In any other python files includes the `if` will fail and `main()` will not be called. This allows us to use that `if` statement and `main()` definition in every file. In top level python file this will cause the application to run, but we can use it in additional files to test and/or demonstrate the functionality of those files.*

*Imagine a project with two files `myApp.py` and `myTables.py`. `myApp.py` contains the bulk of your application. It uses `myTables.py` to generate a bunch of tables. You launch the application with `python myApp.py`, Python finds the if in `myApp.py`, calls the `main()` in `myApp.py` and runs the application, which uses `myTables.py` to create tables. The `if` in `myTables.app` fails and the `main()` in `myTables.py` does not get called.* 

*We can also run `python myTables.py`. This will not run the application. Instead it runs the `main()` in `myTables.py`. This might demonstrate that `myTables.py` is working correctly by creating a collection of tables and output them to the screen.*

## Comments

Comments begin with `#` and continue to the end of the line
```python
# This is a comment
print("Hello") # So is this
```

## No Semi-colons (;) at the end of lines

Lines of code in Python **do not need to** end with a semi-colon.  
```python
# Correct
print("Hello")
# Not incorrect but considered improper
print("Hello");
print("hello"); print("world")
```
You can use a semi-colon to write two commands on one line. Using it at the end of the line will work but is considered bad practice.  

## Scope In Python
Scope in Python is defined by indentations. All the code in a function is indented. In an if statement all the indented code is part of the if. `{}` brackets are **not** used for scope.

```python
def helloWorld():
  print("Hello World!") # Part of the function
  print("Hello Mum!") # Part of the function
  print("Hello Dat!") # Part of the function

print("Hello YSJ") # Not part of the function

if name == "Andy":
  print("Hello Andy")
  print("How are you?")

print("Not part of if()")
```

## Variables In Python

In Python you do not declare variables. You simply start using them. Python determines the type of a variable when a value is first assigned to it.  
```python
x = 5
y = "John"
print(x)
print(y)
```
`x` becomes an integer when the value 5 is assigned to it. `y` becomes a string when "John" is assigned to it.  

Python types are not even fixed, they can and will change if you assign a different type of data to them.  
```python
x = 4 # x is of type int
x = "Sally" # x is now of type str
print(x)
```
Strings can be indicated by single or double quotes. `"John"` is the same as `'John'`.  

### Variable Names
A variable can have a short name (like x and y) or a more descriptive name (age, carname, total_volume).  
Rules for Python variables: 
* A variable name must start with a letter or the underscore character
* A variable name cannot start with a number
* A variable name can only contain alpha-numeric characters and underscores (A-z, 0-9, and _ )
* Variable names are case-sensitive (age, Age and AGE are three different variables)

### Multiple Assignment To Variables
Python allows you to assign a single value to several variables simultaneously. For example −  
`a = b = c = 1`  
Here, an integer object is created with the value 1, and all three variables are assigned to the same memory location.  

You can also assign multiple objects to multiple variables. For example −  
`a,b,c = 1,2,"john"`  
Here, two integer objects with values 1 and 2 are assigned to variables a and b respectively, and one string object with the value "john" is assigned to the variable c.  

## Strings In Python
Strings in Python are identified as a contiguous set of characters represented in the quotation marks. Python allows for either pairs of single or double quotes. Subsets of strings can be taken using the slice operator ([ ] and [:] ) with indexes starting at 0 in the beginning of the string and working their way from -1 at the end.  

The plus (+) sign is the string concatenation operator and the asterisk (*) is the repetition operator. For example −  

```python
str = 'Hello World!'

print str          # Prints complete string
print str[0]       # Prints first character of the string
print str[2:5]     # Prints characters starting from 3rd to 5th
print str[2:]      # Prints string starting from 3rd character
print str * 2      # Prints string two times
print str + "TEST" # Prints concatenated string
```
This will produce the following result −  
```console
Hello World!
H
llo
llo World!
Hello World!Hello World!
Hello World!TEST
```

## Type Conversion
While Python variable have no fixed type it is sometimes useful to ensure data has a specific type. Python provides conversion functions for this purpose.  

* int(x [,base]) - Converts x to an integer. base specifies the base if x is a string.
* long(x [,base] ) - Converts x to a long integer. base specifies the base if x is a string.
* float(x) - Converts x to a floating-point number.
* complex(real [,imag]) - Creates a complex number.
* str(x) - Converts object x to a string representation.
* repr(x) - Converts object x to an expression string.
* eval(str) - Evaluates a string and returns an object.
* tuple(s) - Converts s to a tuple.
* list(s) - Converts s to a list.
* set(s) - Converts s to a set.
* dict(d) - Creates a dictionary. d must be a sequence of (key,value) tuples.
* frozenset(s) - Converts s to a frozen set.
* chr(x) - Converts an integer to a character.
* unichr(x) - Converts an integer to a Unicode character.
* ord(x) - Converts a single character to its integer value.
* hex(x) - Converts an integer to a hexadecimal string.
* oct(x) - Converts an integer to an octal string.




