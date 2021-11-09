---
title: Introduction
permalink: /docs/despat-0-intro/
---

[Video of lecture](https://web.microsoftstream.com/video/ee05df38-6c6e-433f-900e-1f07542112d6)  

## Design Patterns

Design patterns represent the best practices used by experienced object oriented software developers. They are solutions to general problems that software developers faced during software development. These solutions were obtained by trial and error by numerous software developers over quite a substantial period of time.

## The Gang Of Four

In 1994, four authors Erich Gamma, Richard Helm, Ralph Johnson and John Vlissides published a book titled Design Patterns - Elements of Reusable Object-Oriented Software which initiated the concept of the Design Pattern in Software development. These authors are collectively known as Gang of Four (GOF). According to these authors design patterns are primarily based on the following principles of object orientated design.
* Program to an interface not an implementation
* Favour object composition over inheritance

## Design Pattern Usage

Design Patterns have two main uses in software development.
* Common platform for developers
  * Design patterns provide a standard terminology and are specific to particular scenario. For example, a singleton design pattern signifies use of single object so all developers familiar with single design pattern will make use of single object and they can tell each other that program is following a singleton pattern.
* Best Practices
  * Design patterns have been evolved over a long period of time and they provide best solutions to certain problems faced during software development. Learning these patterns helps unexperienced developers to learn software design in an easy and faster way.

## Types Of Design Patterns

### From The GOF

The Gang of Four described patterns belonging to three categories in their book.

* **Creational Patterns** - These design patterns provide a way to create objects while hiding the creation logic, rather than instantiating objects directly using new operator. This gives program more flexibility in deciding which objects need to be created for a given use case.
* **Structural Patterns** - These design patterns concern class and object composition. Concept of inheritance is used to compose interfaces and define ways to compose objects to obtain new functionalities.
* **Behavioural Patterns** - These design patterns are specifically concerned with communication between objects.

<centre>        
    <img src="{{ "/assets/img/dpintro/gof.png" | relative_url }}" alt="Design Patterns Categories" class="img-responsive">
</centre>

### Other Types
* **Concurrency Patterns** - These those types of design patterns that deal with the multi-threaded programming paradigm.
* **Game Patterns** - Not really a full category but we will look at some game specific patterns.  

## Benefits

Design patterns help to solve common design problems through a proven approach.  

They are well documented so that there is no ambiguity in the understanding and they may help reduce the overall development time because rather than finding a solution you are applying a well known solution.  

Design patterns promote code reusability and loose coupling within the system. This helps deal with future extensions and modifications with more ease than otherwise.  

Design patterns promote clear communication between technical team members due to their well documented nature. Once the team understands what a particular design pattern means, its meaning remains unambiguous to all the team members.  

Design patterns may reduce errors in the system since they are proven solutions to common problems.  

## Quick Examples

### The Mediator Pattern

Imagine you have a game or application with multiple screens. You want to be able to switch from one screen to any other.  

<centre>        
    <img src="{{ "/assets/img/dpintro/mediator1.png" | relative_url }}" alt="Mediator Pattern" class="img-responsive">
</centre>

We would rather not hard-code all the possible options for the other screens in to each screen. That would be a lot of repeated code and a lot of work if we add a new screen. Instead we create a mediator, a single object that knows about all the screens. The screens now let the mediator handle the scree swapping. No repetition of code. Far easier to maintain.  

<centre>        
    <img src="{{ "/assets/img/dpintro/mediator2.png" | relative_url }}" alt="Mediator Pattern" class="img-responsive">
</centre>

### The Adapter Pattern

Imagine you have a system set up to handle a stream of objects.  

<centre>        
    <img src="{{ "/assets/img/dpintro/adapter1.png" | relative_url }}" alt="Adapter Pattern" class="img-responsive">
</centre>


But after a system upgrade to handle new objects, the few remaining old objects are no longer compatible.  

<centre>        
    <img src="{{ "/assets/img/dpintro/adapter2.png" | relative_url }}" alt="Adapter Pattern" class="img-responsive">
</centre>

The adapter pattern provides a solution.  

<centre>        
    <img src="{{ "/assets/img/dpintro/adapter3.png" | relative_url }}" alt="Adapter Pattern" class="img-responsive">
</centre>

### The Observer Pattern

Imagine you have an object that is storing data the gets updated with no fixed timing. Other objects need some or all of that data and need the latest data. One option is for the other objects to constant check on the data but that's a lot of checking for something that might not be updated very often. We don't want to hard-code connections in to the original object either.  

Instead the Observer pattern gives a way for the other objects to register themselves with the original and receive automated updates when the data changes.  

<centre>        
    <img src="{{ "/assets/img/dpintro/observer1.png" | relative_url }}" alt="Observer Pattern" class="img-responsive">
</centre>

<centre>        
    <img src="{{ "/assets/img/dpintro/observer2.png" | relative_url }}" alt="Observer Pattern" class="img-responsive">
</centre>

<centre>        
    <img src="{{ "/assets/img/dpintro/observer3.png" | relative_url }}" alt="Observer Pattern" class="img-responsive">
</centre>

## Design Pattern Principles

The two main principles, identified by the Gang of Four, behind Design Patterns are
* program to an interface not an implementation
* favour object composition over inheritance
What do these actually mean?

### Program To An Interface Not An Implementation

At its core "program to an interface" means focusing your design on **what** the code is doing, not **how** it does it.  

As Telastyn puts it in an answer on Stack Exchange  

> The main idea is that domains change far slower than software does. Say you have software to keep track of your grocery list. In the 80's, this software would work against a command line and some flat files on floppy disk. Then you got a UI. Then you maybe put the list in the database. Later on it maybe moved to the cloud or mobile phones or facebook integration.
>
>If you designed your code specifically around the implementation (floppy disks and command lines) you would be ill-prepared for changes. If you designed your code around the interface (manipulating a grocery list) then the implementation is free to change.

This is a *top-down* approach to design and coding. We begin by identifying what classes/objects we need and then identify which classes will interact. We go on to identify what attributes each class should have and what we expect each class to do. Which is to say its methods, or at least those methods required to fulfil its role.  

Java provides an **Interface** class type which allows you to specify methods a class must implement. The Interface can be used in addition to inheritance - class can be a sub-class and implement an interface. Indeed the reason Java has Interfaces is that it does have multiple inheritance. A class in Java can inherit from a single parent class only.  

However a formal **Interface** is not required to follow this principle. Python does not have (as part of core Python) an Interface. Python does allow inheritance from multiple classes though, the interface can be inherited from one or more classes. 

Which leads nicely in to the second principle.  

### Favour Object Composition Over Inheritance

Inheritance is a powerful, useful tool but it has its problems. One problem that can arrive is a proliferation of classes.  

An object oriented solution to a problem might have a super-class with a number of sub-classes and even sub-sub-classes. This can be an ideal solution when it allows us to move common functionality to a higher level so we don't need to repeat code in multiple places. Code that only resides in one class is easier to maintain.  

Take the classic object-oriented example of animals in a zoo. We might have a top level class called *animal*, it stores data like food eaten, location, keeper. Every creature in the zoo has those attributes. Inheriting from *animal* we have sub-classes for *bird*. *reptile*, *fish* and *mammal* and we store information related to those types of animals in those classes.  
But lets look at it from another angle. Our zoo simulation needs other data and functionality. If we are going to simulate those animals we'll need to know which ones swim, fly or walk. This causes us a problem. Not all birds fly and not all flying creatures are birds so if we add *fly()* to the *bird* class we'll have to have a subclass for non-flying-birds which turns it off again. Plus we'll have to add *fly()* to bats and any insects. Now the *fly()* code is all over the place, if we change it we'll have to change it in many places. We'd have the same problems with *swim* and *run*. And that's all before we start looking at marsupials that are warm blooded and lay eggs!  

The alternative to inheritance is composition. With composition we can build objects from a selection of objects of other classes. These other classes are focused on a single specific concept. With our zoo example we would still have an *animal* class containing all the data that is applicable to every animal but we might have classes for *flier*, *egg layer*, *swimmer*, *carnivore*, etc. Then we want to create a *penguin* we use the *animal* class but add in *swimmer*, *egg layer* and *carnivore*. To create a *pigeon* we only use *flier* and *egg layer*.  

We *could* do this in Python by using multiple inheritance and many parents but composition is the approach favoured in the design pattern approach.  

