---
title: Python More Advanced OOPs
permalink: /docs/pyoops-2/
---

## Multiple Inheritance

Java only allows inheritance from a single parent class. Python, like C++, allows inheritance from multiple parent classes. 

```python
class Base1:
    pass

class Base2:
    pass

class MultiDerived(Base1, Base2):
    pass
```

![Multiple Inheritance](/assets/img/minherit.jpg "Inheriting from multiple parent classes")

The `MultiDerived` class inherits from both `Base1` and `Base2` classes.  

### Method Resolution Order

In the multiple inheritance scenario, any specified attribute is searched first in the current class. If not found, the search continues into parent classes in depth-first, left-right fashion without searching the same class twice.  

So, in the above example of `MultiDerived` class the search order is `[MultiDerived, Base1, Base2, object]`. This order is also called linearization of `MultiDerived` class and the set of rules used to find this order is called **Method Resolution Order (MRO)**.

MRO must prevent local precedence ordering and also provide monotonicity. It ensures that a class always appears before its parents. In case of multiple parents, the order is the same as tuples of base classes.

MRO of a class can be viewed as the `__mro__` attribute or the `mro()` method. The former returns a tuple while the latter returns a list.

```python
MultiDerived.__mro__
(<class '__main__.MultiDerived'>,
 <class '__main__.Base1'>,
 <class '__main__.Base2'>,
 <class 'object'>)

MultiDerived.mro()
[<class '__main__.MultiDerived'>,
 <class '__main__.Base1'>,
 <class '__main__.Base2'>,
 <class 'object'>]
 ```

 Multiple inheritance can get very involved..  

![Multiple Inheritance](/assets/img/minherit2.jpg "Inheriting from multiple parent classes")

## Operator Overloading

To overload the + operator, we will need to implement `__add__()` function in a class.

```python
class Point:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def __str__(self):
        return "({0},{1})".format(self.x, self.y)

    def __add__(self, other):
        x = self.x + other.x
        y = self.y + other.y
        return Point(x, y)
```

```python
p1 = Point(1,2)
p2 = Point(4,2)
p3 = p1 + p2
```

### Arithmetic Operators

|Operator|Expression|Internally|
|---|---|---|
|Addition|p1 + p2|p1.__add__(p2)|
|Subtraction|p1 - p2|p1.__sub__(p2)|
|Multiplication|p1 * p2|p1.__mul__(p2)|
|Power|p1 ** p2|p1.__pow__(p2)|
|Division|p1 / p2|p1.__truediv__(p2)|
|Floor Division|p1 // p2|p1.__floordiv__(p2)|
|Remainder (modulo)|p1 % p2|p1.__mod__(p2)|
|Bitwise Left Shift|p1 << p2|p1.__lshift__(p2)|
|Bitwise Right Shift|p1 >> p2|p1.__rshift__(p2)|
|Bitwise AND|p1 & p2|p1.__and__(p2)|
|Bitwise OR|p1 \| p2|p1.__or__(p2)|
|Bitwise XOR|p1 ^ p2|p1.__xor__(p2)|
|Bitwise NOT|~p1|p1.__invert__()|

