---
title: Refactoring
permalink: /docs/other-1/
---

**Code refactoring** is the process of restructuring existing computer code—changing the factoring—without changing its external behaviour. Refactoring improves non-functional attributes of the software.  

This is done to 
* Improve code readability
* Reduce complexity
* Improve source-code maintainability
* Improve architecture/object model to improve extensibility

It is typically carried out as a series of micro-refactoring each of which is usually a tiny change in code that preserves behaviour of the software or at least does not modify its performance to functional requirements.  

## Preparation
Before refactoring a section of code, a solid set of automatic unit tests is needed. The unit tests are used to demonstrate the correct functionality of the original code and then demonstrate that the refactoring has not changed the functionality of the code. The unit-tests therefore need to be thorough and complete, testing all the functionality fully.  

## Refactoring Techniques

You may notice that some of these techniques seem to be the opposite of other techniques. This is because they are. There isn't always one best way to do things. 

### Composing Methods
Much of refactoring is devoted to correctly composing methods. In most cases, excessively long methods are the root of all evil. The vagaries of code inside these methods conceal the execution logic and make the method extremely hard to understand – and even harder to change.  

The refactoring techniques in this group streamline methods, remove code duplication, and pave the way for future improvements.  

#### Extract Method

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
You have a code fragment that can be grouped together  

```python
def printOwing():
    printBanner()

# Print details
print("Name : ", self.name
print("Amount : ", getOutstanding())
```
Why? – the more lines in a method, the harder it is to figure out what a method does.  
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Move this code to a separate, new method

```python
def printOwing():
    printBanner()
    printDetails(getOutstanding())

def printDetails(outstanding):
print("Name : ", self.name
print("Amount : ", outstanding)
```  
</div>
</div>

#### Inline Temp

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
You have a temporary variable that is assigned the result of a simple expression and nothing more

```python
def hasDiscount(order):
    basePrice = order.basePrice()
    return (basePrice > 1000)
```
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Replace the references to the variable with the expression itself

```python
def hasDiscount(order):
    return (order.basePrice > 1000)
```  
</div>
</div>

#### Split Temporary Variable

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
You have a local variable that is used to store various intermediate values inside a method

```python
double temp = 2 * (height + width)
print(temp)
temp = height * width
print(temp)
```
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Use different variables for different values. Each variable should be responsible for only one particular thing.

```python
double perimeter = 2 * (height + width)
print(perimeter)
area = height * width
print(area)
```  
</div>
</div>

#### Other Composing Methods
* Inline Method
* Extract Variable
* Replace Temp with Query
* Remove Assignments to Parameters
* Replace Method with Method Object
* Substitute Algorithm

### Moving Features Between Objects

Even if you have distributed functionality among different classes in a less-than-perfect way, there is still hope.  

These refactoring techniques show how to safely move functionality between classes, create new classes, and hide implementation details from public access.  

#### Extract Class

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
When one class does the work of two, awkwardness results

<img src="/assets/img/other/extractclass1.png" alt="Too busy class">
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Instead, create a new class and place the fields and methods responsible for the relevant functionality in it.

<img src="/assets/img/other/extractclass2.png" alt="Better classes">
</div>
</div>

#### Hide Delegate

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
The client gets object B from a field or method of object A. Then the client calls a method of object B

<img src="/assets/img/other/hidedelegate1.png" alt="Hide delegate">
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Create a new method in class A that delegates the call to object B. Not the client does not know about, or depend on, class B

<img src="/assets/img/other/hidedelegate2.png" alt="Hide delegate">
</div>
</div>

#### Other Techniques
* Move Method
* Move Field
* Inline Class
* Remove Middle Man
* Introduce Foreign Method
* Introduce Local Extension

### Organising Data

These refactoring techniques help with data handling, replacing primitives with rich class functionality. Another important result is untangling of class associations, which makes classes more portable and reusable.  

#### Self Encapsulate Field

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
You use direct access to private fields inside a class

</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Create a getter and setter for the field, and use only them for accessing the field.

</div>
</div>

#### Replace Array With Object

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
You have an array that contains various types of data.

```python
data = ["Liverpool",15]
```
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Replace the array with an object that will have separate fields for each element

```python
data = Address("Liverpool", "15")
```  
</div>
</div>

#### Other Techniques
* Replace Data Value with Object
* Change Value to Reference
* Change Reference to Value
* Duplicate Observed Data
* Change Unidirectional Association to Bidirectional
* Change Bidirectional Association to Unidirectional
* Replace Magic Number with Symbolic Constant
* Encapsulate Field
* Encapsulate Collection
* Replace Type Code with Class
* Replace Type Code with Subclasses
* Replace Type Code with State/Strategy
* Replace Subclass with Fields

### Simplifying Conditional Expressions
 
Conditionals tend to get more and more complicated in their logic over time, and there are yet more techniques to combat this as well.  

#### Decompose Conditional

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
You have a complex conditional

```python
if date.before(SUMMER_START) or date.after(SUMMER_END):
    charge = quantity * winterRate
else:
    charge = quantity * summerRate
```
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Decompose the complicated parts of the conditional into separate methods.

```python
if date.notSummer():
    charge = winterCharge(quantity)
else:
    charge = summerCharge(quantity)
```  
</div>
</div>

#### Replace Nested Conditional with Guard Clauses

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
You have a group of nested conditionals and it is hard to determine the normal flow of code execution.

```python
def getPayAmount():
  result = 0
  if isDead:
    result = deadAmount()
  else:
    if isSeparated:
      result = separatedAmount()
    else:
      if isRetired:
        result = retiredAmount()
      else:
        result = normalPayAmount()
  return result
```
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Isolate all special checks and edge cases into separate clauses and place them before the main checks. Ideally, you should have a "flat" list of conditionals, one after the other.

```python
def getPayAmount():  
  if isDead:
    return deadAmount()
  if isSeparated:
    return separatedAmount()
  if isRetired:
    return retiredAmount()
  return normalPayAmount()
```  
</div>
</div>

#### Other Techniques

* Consolidate Conditional Expression
* Consolidate Duplicate Conditional Fragments
* Remove Control Flag
* Replace Conditional with Polymorphism
* Introduce Null Objects
* Introduce Assertion

### Simplifying Method Calls

These techniques make method calls simpler and easier to understand. This, in turn, simplifies the interfaces for interaction between classes.

#### Rename Method

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
The method name does not explain what the method does
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Rename the method to an explanatory name
</div>
</div>

#### Introduce Parameter Object

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
Your method includes repeating groups of parameters

<img src="/assets/img/other/introparameter1.png" alt="Repeated Parameters">
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Replace these parameters with an object

<img src="/assets/img/other/introparameter2.png" alt="Parameter Object">
</div>
</div>

#### Other Techniques

* Add Parameter
* Remove Parameter
* Separate Query from Modifier
* Parameterise Method
* Replace Parameter With Explicit Methods
* Preserve Whole Object
* Replace Parameter with Method Call
* Remove Setting Method
* Hide Method
* Replace Constructor with Factory Method
* Replace Error Code With Exception
* Replace Exception with Test

### Dealing With Generalisation

Abstraction has its own group of refactoring techniques, primarily associated with moving functionality along the class inheritance hierarchy, creating new classes and interfaces, and replacing inheritance with delegation and vice versa.

#### Pull Up Field

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
Two classes have the same field

<img src="/assets/img/other/pullup1.png" alt="Repeated Parameters">
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Remove the field from the subclasses and move to the superclass

<img src="/assets/img/other/pullup2.png" alt="Parameter Object">
</div>
</div>

#### Extract Subclass

<div class="row">
<div class="col-md-6"  markdown="1">
**Problem**  
A class has features that are only used in certain cases

<img src="/assets/img/other/extractclass1.png" alt="Repeated Parameters">
</div>
<div class="col-md-6"  markdown="1">
**Solution**  
Create a subclass and use it in those cases

<img src="/assets/img/other/extractclass2.png" alt="Parameter Object">
</div>
</div>

#### Other Techniques
* Pull Up Method
* Pull Up Constructor Body
* Push Down Method
* Push Down Field
* Extract Superclass
* Extract Interface
* Collapse Hierarchy
* Form Template Method
* Replace Inheritance With Delegation
* Replace Delegation with Inheritance

## Summary

Refactoring is the process of improving code without changing functionality. Its purpose is to improve readability and increase reusability


