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

### Composing Methods
Much of refactoring is devoted to correctly composing methods. In most cases, excessively long methods are the root of all evil. The vagaries of code inside these methods conceal the execution logic and make the method extremely hard to understand – and even harder to change.  

The refactoring techniques in this group streamline methods, remove code duplication, and pave the way for future improvements.  

#### Extract Method
<div class="row">
<div class="column" markdown="1">
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
<div class="column"  markdown="1">
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









<div class="row">
<div class="column" markdown=1>
LHS
</div>
<div class="column" markdown=1>
RHS
</div>
</div>

<img src="/assets/img/other/blob.jpg" alt="The Blob!">


