---
title: Functions
permalink: /docs/py-4/
---

## Defining Functions

A function is defined using the `def` keyword.

```python
def functionName(arguments):
  # code indented

  return value # optional
```

Note we are not defining a return type (or even if there is a return type) or the types of the parameters. Types will be assigned each time the function is called.  

### Default Parameters

We can define default values for parameters. These values will be used if the parameter is not passed.  

```python
def multi_print(print_me, times=4):
  if times > 0:
    for x in range(times):
      print(print_me)

multi_print("Hello",3)
multi_print("Bye")
```
```console
Hello
Hello
Hello
Bye
Bye
Bye
Bye
```

Note that default values are evaluated at the point the function is defined.  
```python
i = 5

def f(arg=i):
    print(arg)

i = 6
f()
```
will print `5`.

### Keyword Arguments

When you call a function you can specify which parameters you are passing  
```python
def multi_print(word1, print_count=1, tab_count=0):
  outstring = ""
  for b in range(tab_count):
    outstring = outstring +"\t"
  outstring = outstring + word1
  for a in range(print_count):
    print(outstring)

multi_print("Hello")

multi_print("Bye",2)

multi_print("Wow", tab_count=2)

multi_print("Boo", tab_count=3, print_count=3)

```

Produces  

```console
Hello
Bye
Bye
    Wow
      Boo
      Boo
      Boo
```


#### Exercise 1 

1. Log in to replit.com
2. Go to [https://replit.com/@andyguest/pyFunctions](https://replit.com/@andyguest/pyFunctions)
3. Click on the `fork` button at the top of the window to make a copy of the code in your own repls
4. Click on the three lines at the top left of the window and then `My Repls` in the pop out menu
5. Open the `pyFunctions` repl from your area
6. Work your way through the tasks in the code - they are in the comments