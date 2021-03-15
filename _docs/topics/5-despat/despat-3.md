---
title: Composition vs Inheritance
permalink: /docs/despat-3/
---

## The Strategy Pattern

The Strategy pattern is a good way to show the difference between composition and inheritance. This page will work through a problem using inheritance and then using composition. Along the way we'll have a look at the Strategy pattern.

The Strategy pattern describes how to extract volatile parts of your code and encapsulate them as objects so you can use those objects as you need them

<centre>        
    <img src="{{ "/assets/img/dpintro/strategy1.png" | relative_url }}" alt="The Strategy Pattern" class="img-responsive">
</centre>

### The Inheritance Approach

We can replicate the Strategy pattern, which uses composition, by instead using inheritance. In doing so we'll see why the composition approach of design patterns is a cleaner way of working.  

Imagine a race game featuring different types of vehicles. We start with a simple generic *Vehicle* class. 

```python
class Vehicle:
  def __init__(self):
    pass
  def go(self):
    print("Now I'm driving")
```

We want to add some varieties of cars, so we create specific child classes.  

```python
class StreetRacer(Vehicle):
  def __init__(self):
    pass

class FormulaOne(Vehicle):
  def __init__(self):
    pass
```

In our main.py we create objects of both vehicles and make them move. (Just pretend `go()` is doing something a bit more exciting than printing out text!).

```python
from vehicle import StreetRacer, FormulaOne

streetRacer = StreetRacer()
formulaOne = FormulaOne()

streetRacer.go()
formulaOne.go()
```

Somewhere along the line the scope of our game changes and we need to add helicopters and jets. No problem, we create a couple of new classes and update main.py.  

```python
class Helicopter(Vehicle):
  def __init__(self):
    pass

class Jet(Vehicle):
  def __init__(self):
    pass

from vehicle import StreetRacer, FormulaOne, Helicopter, Jet

streetRacer = StreetRacer()
formulaOne = FormulaOne()
helicopter = Helicopter()
jet = Jet()

streetRacer.go()
formulaOne.go()
helicopter.go()
jet.go()
```

```console
Now I'm driving
Now I'm driving
Now I'm driving
Now I'm driving
```

Hmm, not exactly what we want, but we've got inheritance, we can over-ride `go()` in `Helicopter` and `Jet`.  

```python
class Helicopter(Vehicle):
  def __init__(self):
    pass
  def go(self):
    print("Now I'm flying")

class Jet(Vehicle):
  def __init__(self):
    pass
  def go(self):
    print("Now I'm flying")
```

```console
Now I'm driving
Now I'm driving
Now I'm flying
Now I'm flying
```

Much better. Only thing is we've started to make things difficult for ourselves in the future. If I need to change the driving `go()` works, that's fine, I just change the `go()` in `Vehicle`. If I want to change how flying works though I'll need to change it in both `Helicopter` and `Jet`. I might be able to handle making the same change in two places but I'm hoping this game will be a huge success and I'll be able to make a fortune selling difference vehicle DLC packs! Looking forward I can imagine having a huge tree of classes with functionality repeated all over the place. I need a solution that reduces the repetition of code.  

## The (Actual) Strategy Using Composition

So how does the Strategy pattern tell us to solve this problem. Well it identifies that the `go()` method is the part that changes most and suggests the solution is to remove that `go()` method from the vehicle classes.  

First we create an abstract `GoAlgorithm` class. Don't worry about the `abc` stuff for the time being, that's Python's abstract technique. We'll look at `abc` later.  

```python
import abc

class GoAlgorithm(object):
  __metaclass__ = abc.ABCMeta

  @abc.abstractmethod
  def go(): 
    """Required Method"""

class GoByDrivingAlgorithm(GoAlgorithm):
  def go(): 
    print("Now I'm driving")

class GoByFlyingAlgorithm(GoAlgorithm):
  def go(): 
    print("Now I'm flying")

class GoByFlyingFastAlgorithm(GoAlgorithm):
  def go(): 
    print("Now I'm flying fast")
```

Now we have to modify the `Vehicle` class to have a method to set the `GoAlgorithm` we want to use.

```python
class Vehicle:
  def __init__(self):
    pass
  def setGoAlgorithm(self, go_Algorithm):
    self.go_strat = go_Algorithm
  def go(self):
    self.go_strat.go()
```

We also remove the `Helicopter` and `Jet` `go()` code as it is no longer needed.

Finally, back in main.py, we set everything up and run.

```python
from vehicle import StreetRacer, FormulaOne, Helicopter, Jet
from goalgorithm import GoByDrivingAlgorithm, GoByFlyingAlgorithm, GoByFlyingFastAlgorithm

drive_algorithm = GoByDrivingAlgorithm()
fly_algorithm = GoByFlyingAlgorithm()
flyfast_algorithm = GoByFlyingFastAlgorithm()

streetRacer = StreetRacer()
formulaOne = FormulaOne()
helicopter = Helicopter()
jet = Jet()

streetRacer.setGoAlgorithm(drive_algorithm)
formulaOne.setGoAlgorithm(drive_algorithm)
helicopter.setGoAlgorithm(fly_algorithm)
jet.setGoAlgorithm(flyfast_algorithm)

streetRacer.go()
formulaOne.go()
helicopter.go()
jet.go()
```

```console
Now I'm driving
Now I'm driving
Now I'm flying
Now I'm flying fast
```

Now we have a solution with no repeated code!  

Even better we can dynamically change the method of movement in the code at runtime. Consider the code below.  

```python
drive_algorithm = GoByDrivingAlgorithm()
fly_algorithm = GoByFlyingAlgorithm()
flyfast_algorithm = GoByFlyingFastAlgorithm()

jet = Jet()

# Jet will taxi down runway
jet.setGoAlgorithm(drive_algorithm)
jet.go()

# Jet takes off
jet.setGoAlgorithm(fly_algorithm)
jet.go()

# Jet goes supersonic
jet.setGoAlgorithm(flyfast_algorithm)
jet.go()
```

Note that the `drive_algorithm` variable (and similar variables) aren't required.  

```python
drive_algorithm = GoByDrivingAlgorithm()
streetRacer.setGoAlgorithm(drive_algorithm)
```

Can be written as 

```python
streetRacer.setGoAlgorithm(GoByDrivingAlgorithm())
```

It is largely a matter of taste which you use.  

[Code from this page](https://replit.com/@andyguest/pyCompVInherit)

