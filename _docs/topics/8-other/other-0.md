---
title: Anti-Patterns
permalink: /docs/other-0/
---

An anti-pattern is a frequently used but largely ineffective solution to a problem.   

Just as a viable pattern describes the way from a problem to a valid solution, an anti-pattern describes the way from a problem to a poor solution. Furthermore, by adding more difficulties to the ones that originally existed, an anti-pattern may leave you in a worse position than before you started.  

The good news is the description of an anti-pattern will include ways to recover from the situation.  

## Patterns vs Anti-Patterns

* Patterns – the benefits exceed the consequences  
* Anti-patterns – the consequences exceed the benefits

Remember that the benefits and consequences are both context dependent. A perfectly good pattern can be an anti-pattern if it is a bad solution to a problem. A solution to a problem can work but still be a bad solution if it causes even more problems.  

Correctly using a design pattern provides us the benefits of not only a solution but also the wealth of knowledge and experience that went in to the development of that pattern.  

Awareness of anti-patterns gives us the insight of developers who have encountered these situations before. This will (hopefully) help us avoid making the same mistakes and recover from them when we inevitably do!  

## Anti-Pattern Categories
* Software Development Anti-Patterns
* Software Architecture Anti-Patterns
* Project Management Anti-Patterns

## Software Anti-Patterns

There are many anti-patterns that crop up regularly in the software world. They are not necessarily to be avoided but they are potential problems to be aware of.  

Common anti-patterns include :- 
* Spaghetti Code
* Analysis Paralysis
* Design By Committee
* God Class
* Mythical Man Month

### The Blob / The God Class

<div class="row">
<div class="col-8" markdown="1">
The Blob is found in designs where one class monopolizes the processing, and other classes primarily encapsulate data.   
This Anti-pattern is characterized by a class diagram composed of a single complex controller class surrounded by simple data classes.  
The key problem here is that the majority of the responsibilities are allocated to a single class.  
*Solution* – examine the methods in the god class and identify the “natural homes” for them in the other classes.  
*Causes* – developing code with a procedural mind-set and shoe-horning it in to classes. Development by accumulation over time.  
</div>
<div class="col-4" markdown="1">
<img src="/assets/img/other/blob.jpg" alt="The Blob!">
</div>
</div>


### The Golden Hammer

<div class="row">
<div class="col-8" markdown=1>
A common anti-pattern in industry. A company buys in a software package, often a database, at great expense. The vendor will push for the company to use the package in every situation, often providing extensions to encourage this.  
*“If you have a hammer, everything looks like a nail” *  
That package is seldom the best solution to every problem.  
</div>
<div class="col-4">
<img src="/assets/img/other/goldenhammer.png" alt="The Golden Hammer">
</div>
</div>

### Mushroom Management

<div class="row">
<div class="col-8" markdown=1>
aka Pseudo-Analysis, Blind Development  
*“Keep your developers in the dark and feed them fertilizer”*  
(Not usually phrased as fertilizer!)  
Some managers have a policy of isolating the system developers from the end users, preferring to pass information through managers and analysts. Mushroom managers assume requirements are known and understood at inception and do not change.  
</div>
<div class="col-4">
<img src="/assets/img/other/mushroom.jpg" alt="Mushrooms">
</div>
</div>

### Cover Your Assets
 
Document-driven software processed often produce less than useful requirements and specifications because the authors evade making important decisions. In order to avoid making a mistake, the authors take a safer course and elaborate upon alternatives.  

<img src="/assets/img/other/coverass.jpg" alt="Dilbert">

### Design by Committee

<div class="row">
<div class="col-8" markdown=1>
“A camel is a horse designed by committee”  
A complex software design is the product of a committee process. It has so many features and variations that it is infeasible for any group of developers to realize the specifications in a reasonable time frame.  
Even if the designs were possible, it would not be possible to test the full design due to excessive complexity, ambiguities, over-constraint, and other specification defects. The design would lack conceptual clarity because so many people contributed to it and extended it during its creation.  
</div>
<div class="col-4">
<img src="/assets/img/other/committee.png" alt="Design by Committee">
</div>
</div>

### Reinvent The Wheel

“Our problem is unique, we need a unique solution”  
Software developers are seldom aware of each other’s code and simultaneously develop differing solutions.  
<img src="/assets/img/other/reinvent.png" alt="Reinvent The Wheel">

### Analysis Paralysis

Object-oriented analysis is focused on decomposing a problem into its constituent parts, but there is no obvious method for identifying the exact level of detail necessary for system design.   

Frequently, the focus is shifted from decomposing to a level where the problem can be easily understood by the designers to applying the techniques to achieve the mythical "completeness."  

<img src="/assets/img/other/analysisparalysis.png" alt="Analysis Paralysis">

### Death By Planning

"We can't get started until we have a complete program plan."  
"The plan is the only thing that will ensure our success."  
"As long as we follow the plan and don't diverge from it, we will be successful."  
"We have a plan; we just need to follow it!"  

<img src="/assets/img/other/deathbyplanning.png" alt="eath By Planning">

