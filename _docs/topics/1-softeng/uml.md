---
title: UML - Unified Modelling Language
permalink: /docs/uml/
---

## Introduction

**UML** is a general purpose, developmental modelling language intended to provide a standard way to visualise the analysis and design of a system. UML was created by the Object Managment Group, the 1.0 specifiation draft was published in January 1997.  

UML is linked with object oriented design and analysis. UML makes the use of elements and forms associations between them to form diagrams. Diagrams in UML can be broadly classified as:

1. **Structural Diagrams** – Capture static aspects or structure of a system. Structural Diagrams include: Component Diagrams, Object Diagrams, Class Diagrams and Deployment Diagrams.
2. **Behavior Diagrams** – Capture dynamic aspects or behavior of the system. Behavior diagrams include: Use Case Diagrams, State Diagrams, Activity Diagrams and Interaction Diagrams.

![UML Hierarchy](/assets/img/umlhier.png "UML Hierarchy")

It is beyond the scope of this module to cover every UML diagram. We will focus on those diagrams most useful to us. Below are links to fuller guides if you want information on the other diagrams.

[UML Introduction](https://www.geeksforgeeks.org/unified-modeling-language-uml-introduction/)  
[UML Quick Guide](https://www.tutorialspoint.com/uml/uml_quick_guide.htm)

## Structural UML Diagrams

### Class Diagram

Class Diagrams are probably the most useful to us and the ones we use most frequently. A Class Diagram represents a static view of an application. It shows a collection of classes, interfaces, associations, collaborations, and constraints. It is also known as a structural diagram. They show inheritance, composition, aggregation of classes.  

![UML Class Diagram](/assets/img/uml-class.jpg "UML Class Diagram")

Each class is shown in a standardised form with three sections:-  
1. Name
2. Attributes
  * Data stored as part of the class
3. Operations
  * Class functions  
Attributes and operations may be described as + Public, - Private, # Protected.  

![UML Class Diagram Example](/assets/img/umlclass.png "UML Class Diagram Example")

#### UML Class Relationships

In class diagrams lines drawn between classes describe the relationship between those classes.  
**Instance Level Relationships**
1. Association – shows a connection between the members of two classes
  * Aggregation - implies a relationship where one object can exists independently of the other
  * Composition - implies a relationship where one object cannot exist independently of the other 
2. Inheritance – shows a parent / child relationship
3. Realisation – shows the implementation of an interface
4. Dependency - a relationship where one class uses another by parameter or return type

![UML Class Relationships](/assets/img/umlrel.png "UML Class Relationships")  

#### UML Class Associations

**Association** is a link between members of two classes.
![UML Class Association](/assets/img/umlassoc1.jpg "UML Class Association")  

**Aggregation** – the two classes can exist independently
**Composition** – one class cannot exist independently of the other (within the system) 
![UML Class Association](/assets/img/umlassoc2.png "UML Class Association")  



### Object Diagram

 An Object Diagram is a snapshot of the object instances in a system and the relationship that exists between them. Since object diagrams depict behaviour when objects have been instantiated, we are able to study the behaviour of the system at a particular instant. An Object Diagram represents specific instances of classes and relationships between them at a point of time.  

![UML Object Diagram](/assets/img/uml_object.jpg "UML Object Diagram")

## Behavioural UML Diagrams

### Use Case Diagrams

Use Case Diagrams are used to depict the functionality of a system or a part of a system. They are widely used to illustrate the functional requirements of the system and its interaction with external agents(actors). A use case is basically a diagram representing different scenarios where the system can be used. This gives us a high level view of what the system or a part of the system does without going into implementation details.  

![UML Use Case Diagram](/assets/img/uml_use.jpg "UML Use Case Diagram")

### Sequence Diagram

A sequence diagram simply depicts interaction between objects in a sequential order i.e. the order in which these interactions take place.We can also use the terms event diagrams or event scenarios to refer to a sequence diagram.   

![UML Sequence Diagram](/assets/img/uml_seq.jpg "UML Sequence Diagram")

## UML Notes From Programming 02

[UML From Programming 02](https://ysjprog02.netlify.app/docs/7-uml-1/)