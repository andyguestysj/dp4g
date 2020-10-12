---
title: Design Pattern Types
permalink: /docs/despat-2/
---

We touched on this briefly in the introduction, design patterns (mostly) fall in to three fundamental groups - **behavioural**. **creational** and **structural**.  

## Behavioural Patterns

Behavioural patterns describe interactions between objects and focus on how objects communicate with each other. They can reduce complex flow charts to mere interconnections between objects of various classes. Behavioural patterns are also used to make the algorithm that a class uses simply another parameter that is adjustable at runtime.  

Behavioural patterns are concerned with algorithms and the assignment of responsibilities between objects. Behavioural patterns describe not just patterns of objects or classes but also the patterns of communication between them. These patterns characterize complex control flow that is difficult to follow at run-time. They shift your focus away from the flow of control to let you concentrate just on the way objects are interconnected. Behavioural class patterns use inheritance to distribute behaviour between classes.  

## Creational Patterns
Creational patterns are used to create objects for a suitable class that serves as a solution for a problem. Generally when instances of several different classes are available. They are particularly useful when you are taking advantage of polymorphism and need to choose between different classes at runtime rather than compile time.  

Creational patterns support the creation of objects in a system. Creational patterns allow objects to be created in a system without having to identify a specific class type in the code, so you do not have to write large, complex code to instantiate an object. It does this by having the subclass of the class create the objects. However, this can limit the type or number of objects that can be created within a system.  

## Structural Patterns
Structural patterns form larger structures from individual parts, generally of different classes. Structural patterns vary a great deal depending on what sort of structure is being created for what purpose.  

Structural patterns are concerned with how classes and objects are composed to form larger structures.  

Structural class patterns use inheritance to compose interfaces or implementations. As a simple example, consider how multiple inheritance mixes two or more classes into one. The result is a class that combines the properties of its parent classes. This pattern is particularly useful for making independently developed class libraries work together.  

Patterns may further be divided by their scope - object patterns and class patterns.  

## Object patterns
Object patterns, the more common of the two, specify the relationships between objects. In general, the purpose of an object pattern is to allow the instances of different classes to be used in the same place in a pattern. Object patterns avoid fixing the class that accomplishes a given task at compile time. Instead the actual class of the object can be chosen at runtime. Object patterns mostly use object composition to establish relationships between objects.

## Class patterns
Class patterns specify the relationship between classes and their subclasses. Thus, class patterns tend to use inheritance to establish relationships. Unlike object patterns and object relationships, class patterns generally fix the relationship at compile time. They are less flexible and dynamic and less suited to polymorphic approaches.
