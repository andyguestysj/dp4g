---
title: Object Oriented Analysis & Design
permalink: /docs/ooa/
---

## Object Orientation

The object-oriented approach encourages:  
* Modularisation: where the application can be decomposed into modules.
* Software re-use: where an application can be composed from existing and new modules.

### Modularisation
Object orientation encourages the modularisation of software. By decomposing our application down in to modules we make our code more robust and re-usable. If all the code relating to a single aspect of the application is contained in a single module then we know any problems with that aspect must lie in that module. If we need to make changes to that aspect then we only need to modify one module. Of course we need to be careful that any changes in a single module do not cause problems in other modules. (Which doesn't happen because we're good OO developers that practice good encapsulation, abstraction and polymorphism!).  

### Software Re-use
By careful selection of classes and modularisation we can create modules that can be re-used in other applications. A student class from one application may be re-used in another application with little modification.  

Be aware though. An easy pitfall to fall in to is trying to create the perfect, generic modular version of a class so you can use it over and over again, which can handle any situation without change. Such perfection is almost impossible to achieve in most projects and you will spend far more time trying to create a good generic class than you would creating a new one off class. It takes too long for your current project to support and you seldom benefit in future projects. However if you are developing a programming language or software like a games engine or library, your code should be as modular as possible.

## OO Language Features
An object-oriented programming language generally supports five main features:
* Classes
* Objects
* Classification
* Polymorphism
* Inheritance
These features allow the principles of encapsulation and abstraction to be used.  

To write good object oriented code it is not enough to simply use these features. They must be used properly, with the principles of object orientation kept in mind.  

## Classes
Classes allow us a way to represent complex structures within a programming language.  
They have two components  
* **States** - (or data) are the values that the object has.
* **Methods** - (or behaviour) are the ways in which the object can interact with its data, the actions.
We use UML to illustrate classes

![A Class in UML](/assets/img/class.jpg "A Class in UML")

A class is simply a collection of data and methods. A *good* class should be more than that.  
A good class should :-  
* Provide a well-defined interface - such as the remote control of the television.
* Represent a clear concept - such as the concept of a television.
* Be complete and well-documented - the television should have a plug and should have a manual that documents all features.
* The code should be robust - it should not crash.

### Class Interface
A **class interface** is how an object of that class is created, accessed and deleted. At the simplest level the interface consists of constructors, getters, and setters. Class data should be *Private* so that they can only be accessed through the interface. Data may need to *Protected* for inheritance. (In practice some data is *Public* for ease of use. Some languages, like Python, make all data public, relying on the coders to behave). Note that you do not have to have getters and setters for each data element. Some data is only used by code inside the class and need never be accessed from outside.  
Methods that are the top level functionality of the code will be public too. In the TV example, methods to TurnOnTV() and ChangeChannel() would be public.  

### Clear Concept
A class should have a **clear concept**. Identifying which classes to use in an application is complicated. Two different solutions may use two very different sets of classes. There is no *correct* set of classes for any problem, there are simply *better* and *worse* approaches to use. Learning to distinguish between the two and what makes for better solutions is an important skill for any objeect oriented programmer.  
A **clear concept** is a principle which helps in developing good solutions. A clear concept means that we can understand what the purpose of a class is from its name. We should be able to infer from the name why attributes it has (its data) and what it can do (its methods). Classes *know things* and *do things*. They should only *know things* and *do things* relevant to their concept.  

With our TV example we consider a **remote control class**. The remote control should be able to turn the TV, change channels, change the volume, etc. These days we use the remote to bring up what is on right now across the channels, but is that something the *remote control* does? Or is it something the *TV* does? Either solution could work but if we place the code in the remote control then we are tying the remote control to the TV. Either we need a different remote control for each TV or the remote control needs to know how to work with every TV. A better solution is to put the code in the TV class and have the remote send a generic request for listings to the TV. That way the remote control class works with every TV and each TV can have its own listings approach.  

Some programmers believe that a clear concept requires that each class represents something that exists within the framework of the application or game concept. These may be physical components (TV, remote control) or more conceptual ones (channel, programme, film). Such programmers disapprove of *manager classes*, classes which exists to manage or provide access to a selection of object. Others believe that manager classes are too convenient to ignore and that solutions without them are far more complex. The counter argument to that is that if you have to use a manager class you are using the wrong programming language for your application.  

``` Aside: You will see this argument come up time and time again. OOP principles can be inconvenient if enforced rigourously as rules. Breaking the rules for convenience and simplicity is seen by some as an admission you are using the wrong OOP language. Welcome to the world of software development. Not only do we argue over whether or not OOP is a good thing, we argue over which OOP (or non-OOP) language we should use. ```  

### Complete and well documented
Where possible each class should be complete and fully documented. In practice most classes rely on other classes at some point. This is not a contradiction, each class should contain all the features that are part of its *clear concept*. Any connections to other classes should be through the other classes' *interfaces*.  
We've already discussed how programmers aren't big on writing documentation so why do we say that classes should be well documented? Here we are referring, mostly, to commenting code. Each class should be well commented. The class itself should have comments explaining its purpose and use. Each data item should be described, its purpose identified. Methods should be separated by purpose - interface and internal. Each method should have an overall description, parameters and return values should be explained. The individual lines of code should be commented if need be.  
Any specific links to other objects/classes should be described, especially if changes to one might cause problems to the other.

### Robust Code
Each class should be fully tested to ensure it doesn't break. This means testing all possible variations of use, valid or invalid. Each class should gracefully handle the situation where other objects don't exist. Every car has a steering wheel, you should still test your car class to make sure it doesn't crash the system if it can't find its steering wheel object. You may decide that without the steering wheel the program should stop, if so it should stop cleanly, without corrupting date and giving a meaningful error message.

## Object Oriented Software Development

### Requirements
The first step is the gathering of subject domain knowledge. The subject domain is all the information about the system you are developing, it comes in differnt forms. For a game this is usually a mix of game concept and design (design of game play and rules rather than code design). In software engineering this is usually a real world situation for which the customer wants an application and/or an existing application they want to replace. 
In traditional software engineering we attempt to capture every aspect of the subject domain. We capture not only what the software should do but how it should do it (in terms of process and calculation rather than code). Using Agile methodologies it is usually only the "what does the software need to do" that is captured.
Use cases are generally created during the requirements gathering.

#### Use Cases

A **use case** is a list of actions or event steps typically defining the interactions between a role and a system to achieve a goal. The role might be a human or another external system. Use cases are simple, quick descriptions of the steps involved in a process. 
![Use Case Example](/assets/img/usecase.png "Use Case Example")

### Object Oriented Analysis
The first step in developing good object oriented software is analysing the subject domain to identify which classes are present/required. This is a complex task, but there are methods for doing this and it gets easier with practice.

The starting point for the analysis is usually a text description of the game/software. This will come from the requirements gathering process in industry but you might need to write your own for smaller projects (and uni work!).  

The description describe the game/software at a high level allowing someone unfamiliar with it to understand the concept. It can be helpful if it start ats a high level, describing the types of core functionality and then later on repeats the process by focusing on each core function in turn and going in to more detail.

The desciption should describe *what the player/user does*, *is trying to do* and *why*. You should pay attention to *things* and *actions*. In terms of the text identify the *nouns* (the things) and the *verbs* (the actions). Highlighting them in different colours is a good start.

#### Identifying Objects and Classes 

Take your description and
1. Look for nouns
  * **Proper noun** – Alice, Ace of Hearts – describes an object (incidence of class)
  * **Common noun** – Field officer, playing card, value – describes a class (or attribute)
2. Look for verbs
  * **Doing verb** – creates, submits, shuffles – describes an operation
  * **Being verb** – is a kind of, is one of either – describes inheritance
  * **Having verb** – has, consists of, includes – describes aggregation, composition
  * **Modal verb** – must be – describes a constraint
3. Look for adjectives
  * **adjective** – a yellow ball (i.e. colour) – helps identify an attribute

You should now have a first pass list of classes and objects. We can take a deeper look at our list to improve our understanding.

1. Examine your list of nouns
  * Separate them out in to classes, objects and attributes
  * Which attributes are part of which classes?
  * Which objects are instances of which classes?
2. Examine your verbs	
  * Which doing verbs attach to which classes ?
  * Which being verbs describe a relationship between which classes?
  * Which having verbs describe relationships between which classes?
  * Which modal verbs describe constraints on classes?
  * Which modal verbs describe constraints on objects?
  * Which modal verbs describe constraints on attributes?
  * Which adjectives describe attributes of which classes?

Now go back to your description and read it again looking for :-  
1. Entity objects – represent persistent information in the system
  * Account, player, boss monster
  * Look for terms that are domain specific, recurring nouns, real world entities and activities
2. Boundary objects – represent interactions between user and system
  * Button, form, display, movement keys
  * Identify controls that initiate a use case, data entry forms and windows, system messages to user
3. Control objects – represent the management / control of an activity
  * If a use case is complex and involves many objects, create a control object to manage that case
  * Identify one control object per actor in a use case
  * Life span of control object should last through the use case

At this point you should have a good idea of all the classes in the system/game. You should also have identified some of the methods and data of the classes.

[Identifying Classes](https://www.codeproject.com/Articles/9900/Identifying-Object-Oriented-Classes#:~:text=In%20object%2Doriented%20software%20design,Identifying%20classes%20can%20be%20challenging.)

### Object Oriented Design
Once you have your list of classes you can begin designing your application by working out and documenting how the classes are connected and how and when they interact.   

#### Class Diagram
If you have carried out the OOA correctly you should have what you need to create a UML Class Diagram. A Class Diagram shows all the classes in the application and how they are connected. Note that this diagram shows *classes* and not *objects*. As such it is static, it is correct at any time during the application. (As opposed to an object diagram which is a snap shot of the application at a point in time).  

![Class Diagram](/assets/img/classdiagram.png "Class Diagram")

#### Use Cases, Sequence Diagrams, Object Diagrams
You can now take your *class diagram* and your *use cases* and produce a *sequence diagram* for each use case. A sequence diagram describes how objects interact over time.

![Sequence Diagram](/assets/img/seqdiag.png "Sequence Diagram")  

You may also find *object diagrams* useful in describing the data structure of objects at a snapshot in time.

### Implementation
We now take our design documentation and diagrams and implement them in code.

### Agile Note
The above describes the steps involved in traditional software engineering. Using Agile methodologies the same steps are taken but they are taken iteratively. An initial set of use cases is developed to populate the feature list. The object oriented analysis and design for each use case is not carried out until the sprint that works on that use case.