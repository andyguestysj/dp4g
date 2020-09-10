---
title: Traditional Software Engineering
permalink: /docs/tradeng/
---

## Contents

1. Tradition Software Engineering
2. The Waterfall Model
3. Why Use It?
4. Why Does It Fail?

## Software Engineering

According to Wikipedia  
``` Software engineering (SE) is the application of a systematic, disciplined, quantifiable approach to the development, operation, and maintenance of software, and the study of these approaches; that is, the application of engineering to software ```

Software can get very complex very quickly. It is hard for one person to keep track when developing a large application, when more than one person is working on it it becomes almost impossible. We need a methodology, a sensible approach that ensures everything is done correctly, on time and on budget.  

Early software developers took inspiration from the engineering disciplines where projects are planned out, documented in advance with targets and deadlines and work packaged in to parcels so individual engineers could work on small parts of the project in isolation. This approach was applied to developing software, hence software engineering, to try to manage projects and turn ramshackle ad-hoc software hacking in to a predictable, controllable process.  

This approach has met with mixed success. Sometimes it works well, sometimes it fails miserably.  

Along the way some software developers decided that a different approach might be better. An approach that suited how they liked to work, something more flexible. They came up with the Agile Manifesto, a set of principles on how to approach software development. From this manifesto a number of Agile methodologies were developed. 

Traditional software engineering is still very much in use though. There are circumstances where it is a better approach than an Agile one.

## Traditional or Structured Engineering

Traditional, or structured, engineering, is an approach to managing engineering projects that focuses on preparation and planning before action.  

Simply put, the traditional engineering approach is to consider and document every aspect of a project before any other work takes place. With all the information known it is then possible to plan the project, knowing every action that needs to be taken and when. This allows work to be broken down in to smaller tasks that can be carried out independantly of each other and which can be scheduled so that all pre-requisites are carried out in time to complete every task.  

In civil engineering, as an example, extensive investigation is carried out and documented before building work begins. Everything from the ground conditions, local laws and regulations, weather, population, traffic is documented along side the customers requirements for the building - the number of occupants, office space, power, water, etc. Using this documentation every phase of the building process is planned and scheduled. The foundations need to be laid first but this needs to be coordinated with any underground water, waste and electrical installations. The building frame needs to go up followed by the walls, roofing, windows and doors. Internal walls need coordinating with the installation of electrical wiring and water pipes. And so on.  

The careful documentation and planning allows every task to be identified and scheduled. It enables the creation of work packages detailing individual tasks so that particular workers know everything they need to know about specific tasks.  

If everything goes to plan the building will be completed on time, on budget and to specification. Things doen't always go to plan of course, delays can and do occur, but they occur in known ways and the documentation and plans contain contingency plans to handle many problems and delays. Extra and spare time can be built in to timetables to allow for unexpected, but forseeable, delays.  

## Structured approach to software development

How does this work in software development? It is usually illustrated using the Waterfall Model. 

![The Waterfall Model](/assets/img/wfall1.png "The Waterfall Model")

### Stages

#### 1. Requirements  
The requirements for the software to be created are gathered. This can happen in a number of ways. It often involves working with a customer to determine exactly what the software is supposed to do, to identify and performance requirements, accuracy, etc. During this stage every thing the software/game needs to do, how it should look, how it should perform and any other issues should be identified and recorded.  
#### 2. Design
Once all the requirements have been gathered then the team can confidently design the software. Every aspect of the software is completely designed. The design breaks the software down in to packages that can be assigned to programmers, each package contains all the information required to code the software. More packages are created that cover the integration of packages in to completed software.  
#### 3. Implementation
The packages are assigned to programmers who code them up and integrate them together in to software.  
#### 4. Verification
The software is fully tested to ensure it meets the requirements and any bugs are fixed.  
#### 5. Maintenance
The completed software is handed over to the customer and the project moves over to a maintenance phase.  

### The Waterfall Model

The focus on full and complete documentation leads to what is known as the "Big Design Up Front" approach. Everything should be planned before any code is written. Design can be detailed down to the pseudo-code level. Coding is just converting pseudo-code to real code, it doesn't require a great deal of skill or knowledge.  
So what happens in practice?

#### The *Theory*

![The Waterfall Model](/assets/img/wfall1.png "The Waterfall Model")

We have an approach. We can make a plan, everything will be fine..

#### Problems lead to revisions

![The Waterfall Model](/assets/img/wfall2.png "The Waterfall Model")

Problems can be found at any stage and often are. Occasionally they can be fixed during that stage but if we are strictly applying the approach of documenting and preparing everything we usually need to back track to an earlier stage to ensure the plan is complete and the documentation is up to date.  

#### New Requirements

![The Waterfall Model](/assets/img/wfall3.png "The Waterfall Model")

The initial analysis is never complete. There are items analysts fail to notice, there are requirements that customers forgot about or didn't realise were needed. So we need those requirements to be analysed and documented, the design will need to be updated, code will need to be changed, testing carried out again.  
Software is different from almost any other product. Customers seldom realise how difficult some changes are and ask for the equivalent of seeing an office constructed and wanting it moved three feet to the right. (On the plus side they don't realise how easy other changes are and can be impressed by the smallest things!).  
A big issue is that of knowledge disconnects. Software developers seldom have a good understanding of the business they are developing software for. Similarly the people working in that business seldom know much about developing software. This makes it easy to miss requirements in the early stages.  

#### Serious Flaws/Faulty Requirements

![The Waterfall Model](/assets/img/wfall4.png "The Waterfall Model")

This lack of overlapping knowledge means that not only do requirements sometimes get missed but that requirements are completely. Miscommunications, assumptions about things "so obvious they didn't need to be mentioned", etc lead to situations where the correct approach would be to go back to the start and do everything again.  
Customer testing in the late stages is often where these problems are discovered.

#### Time Pressures

![The Waterfall Model](/assets/img/wfall6.png "The Waterfall Model")

All this reverting to earlier stages and reworking documentation takes time. The pressure to still get the software delivered on time leads to timetable revisions and the time available for each stages gets cut.

#### Delays Lead To Later Delays

![The Waterfall Model](/assets/img/wfall7.png "The Waterfall Model")

Delays in early stages mean subsequent stages start and end later. Plans get further revised and even less time is alloted to tasks.

#### The Spaghetti Model?

![The Waterfall Model](/assets/img/wfall8.png "The Waterfall Model")

Things can easily get out of control..

### Why Does It Fail?

There is a lot of documentation. It can't be done and forgotten about, it must be constantly updated. Any change needs to flow through all the documents. Programmers want to programme. They don't want to spend so much time reading and writing documentation. They also don't like that coding is treated as the smallest, simplest least important role.  

The structured approach isn't flexible. Changes require a lot of back tracking and rework and changes happen very frequently in software development for the reasons discussed earlier.

### Why Use This Approach Then?

Despite the potential flaws the structured approach has a lot going for it. It is easy to understand, it gives plans that are clear to everyone. It is an approach that works well in the other engineering disciplines. It is an approach which works well, or at least well enough, much of the time.  
The alternative, Agile, approaches have a number of issues. They are hard to understand, especially for customers. Agile approaches look like no planning at all to many people. Agile also requires software developers who are knowledgable and experienced to work well.  
Some circumstances like big government contracts have very specific requirements in terms of documentation and planning that mean Agile approached cannot be used.

### What's The Alternative?

Agile approaches offer a different way of working.
