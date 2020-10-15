---
title: Introduction
permalink: /docs/agile-0/
---

## What is Agile?
At its core, Agile is a set of principles that can be used to guide the delivery of a software project. It encourages communication, collaboration and working software over documentation and plans that cannot change.  

## Agile Principles
* **Individuals and interactions** over processes and tools
* **Working software** over comprehensive documentation
* **Customer collaboration** over contract negotiation
* **Responding to change** over following a plan

## Scrum
Scrum is an Agile methodology. Its name comes from the sport of rugby, where a team needs to work together to drive forward and achieve a common goal. It follows the principles set out in the Agile Manifesto, with some additional concepts that sit on top of it, such as Sprints, Product Backlogs and Daily Standups.

[The official Scrum guide is freely available.](../2016-Scrum-Guide-US.pdf)

## Scrum Roles

Within a Scrum project there are a number of key roles that are required :

### Product Owner
The **Product Owner** (PO) is in charge of the project vision. This person is typically somebody senior within a business, who has the authority to make decisions about direction, features and understands the business objectives. Their primary role is to mediate between the internal stakeholders and the Scrum team delivering the project and ensure the team is delivering the most value to the business within each sprint.  
Effective product owners:
* Build and manage the product backlog.
* Closely partner with the business and the team to ensure everyone understands the work items in the product backlog.
* Give the team clear guidance on which features to deliver next.
* Decide when to ship the product with a predisposition towards more frequent delivery.
The product owner is not always the product manager. Product owners focus on ensuring the development team delivers the most value to the business. Also, it's important that the product owner be an individual. No development team wants mixed guidance from multiple product owners.  

### Scrum Master

The **Scrum Master** (SM) handles day-to-day delivery of the sprint. They lead the ceremonies and work closely with the team to remove any blockers that may be impeding progress. The Scrum Master's job is to protect the delivery team and ensure that committed work will be completed for Sprint Showcase. In a well-functioning Scrum team, it's healthy to see a certain amount of tension between the PO and the SM. Naturally, the PO will want more from the scrum team than is feasible and it's the SM's responsibility to help the team deliver consistently and function well.

A **sprint team** consists of people in various roles, such as Software Engineers, Designers, Business Analysts, User Experience and so forth. The team will be required to deliver the sprint and typically work full-time on the Sprint. Sprint teams tend to remain consistent but can change if the user stories being delivered necessitate the change.

## Scrum Development Cycle

<centre>        
    <img src="{{ "/assets/img/agile/scrum.png" | relative_url }}" alt="Scrum Development Cycle" class="img-responsive">
</centre>

## Product Backlog

The first task in any Scrum project is the creation of the **Product Backlog**. 

The **Product Backlog** is the master list of work that needs to get done maintained by the product owner or product manager. This is a dynamic list of features, requirements, enhancements, and fixes that acts as the input for the sprint backlog. It is, essentially, the team’s “To Do” list. The product backlog is constantly revisited, re-prioritized and maintained by the Product Owner because, as we learn more or as the market changes, items may no longer be relevant or problems may get solved in other ways.  

## User Stories

The features in the **produce backlog** are drawn from **User Stories**. A **User Story** is a feature written from a user's 
perspective, for example: "As a Customer, I would like you to remember my credit card details, so I don't have to enter them each time I purchase a product". User stories are preferred to feature lists as they allow the team to more easily understand the business value.  

## Story Points

A **Story Point** is the estimated effort required to complete a **User Story**. It's a relative measure of complexity, rather than some number of hours.

## Sprint 

A **sprint** is a timeboxed period (typically between one and four weeks) where a team commits to completing a set of defined User Stories. A project is comprised of multiple sprints.  

## Sprint Backlog

A **Sprint Backlog** is a list of **User Stories** that the team will aim to complete during a **sprint**. All of the User Stories will have Story Point estimates alongside them, and this total should align with velocity achieved in the previous sprints.

## Spike

A **Spike** is a fixed period used to investigate uncertainty. For example, you could run a 2-day spike to evaluate a new technology that the team hasn't used before.

## Velocity

**Velocity** is the rate at which the team is completing **user stories**. Once a project is underway, and the team is in a rhythm, you would expect to see a consistent **velocity** between **sprints**.

## Planning Poker

Estimating complexity is particularly difficult in software projects. Scrum uses **Planning Poker** to help with this. It's a card game in which the team is given a set of cards, each of which are numbered with a value from a modified version of the Fibonacci sequence: 1, 2, 3, 5, 8, 13, 20, 40 & 100. The numbers get further apart as you get higher to emphasise that bigger things are inherently harder to estimate.The Product Owner describes the User Story and each team member puts a card face down on the table. All cards are turned over simultaneously, and then the team discusses the differences in estimations. This technique encourages discussion and helps to provide fair estimates that the team has agreed upon.

## Blockers

A **blocker** is an impediment that is holding up progress on User Story. For example, if a User Story was to setup Tax Rates for a particular country, but the engineer didn't have this data, the missing data would be considered a Blocker. Blockers should be flagged to the team and if the team cannot resolve them, then the Scrum Master should try to.

## Burndown

The **Burndown** chart visualizes the progress against **velocity** and provides an early warning system if the team are tracking behind the intended target. If a sprint was ten days long, and the team had 100 Story Points to complete, then the team would need to average upwards of 10 points per day to track good progress and see a positive burndown chart.

## Potentially Shipping Increment

A **Potentially Shipping Increment** (PSI) is a piece of functionality which can launch on completion. One of the big focuses in Agile is to limit work in progress and ship frequently. 

## Backlog Grooming

Once a project is underway, it's easy for the **Product Backlog** to grow and grow until it becomes a bit of a mess. One of the tasks for the *Scrum Master* and *Product Owner* (and sometimes the team) is to sit down together, go through the items in the backlog and remove duplicates, or those which are not a priority and are not going to deliver value to the business.

## Sprint Planning

Before a **sprint** begins, it's important that the team are all aligned, and that we have up-to-date story points for the features. The role of the **Sprint Planning** session is to go through the highest priority items in the **Product Backlog** and agree which **User Stories** will be included within the next **Sprint**.

## Ceremonies

Within Scrum, there are ceremonies at key moments in the project. The three main ones being: Daily Standup, Sprint Showcase, and Retrospective.

### Daily Standup

Each morning, the sprint team comes together to have their **Daily Standup**. The standup is a short and informal standing meeting, where the entire team attends. Each team member answers the following three questions:
* What did you complete yesterday?
* What are you going to complete today?
* Is there anything that is blocking you from achieving this?.
Standups are a regular opportunity for the entire team to communicate progress, understand blockers, cross-pollinate information and evaluate risks.

### Sprint Showcase

On sprint completion, a *Sprint Showcase* meeting takes place. In the Showcase, all the *completed User Stories* are showcased to the project stakeholders. The idea behind this session is that the team is sharing what should be a shipping increment, something that the business can release to end consumers and that the business can start seeing some return on their investment from. It's therefore critical that at the end of each sprint, the Scrum team are delivering features that are truly ready to launch.

### Retrospective

*Following Sprint Showcase*, a **Retrospective** is run. This is a fun exercise used to capture feedback from the team on the things that what went well, things that didn't go so well and what learning can be taken into the next sprint. The Agile / Scrum methodologies heavily focus on team improvement and the goal is for the next sprint to be better than the last. This 'always be improving' mentality is key to Agile.

## Scrum In Practice

[Made Tech](www.madetech.com) describe how they put Scrum in to practice as follows.

1. **Before the project starts** – We'll typically run a story planning workshop. In this workshop we'll capture an initial product backlog from the attendees and work together to prioritise stories into an appropriate order.
2. **Before the first sprint** – We'll run a high-level Planning Poker session with the team. We'll add Story Point estimations to the items in the Product Backlog and work with the Product Owner to agree a first sprint.
3. **Sprint starts** – The team will work their way through the User Stories within the Sprint Backlog.
4. **Daily Standups** – Each morning at 10am the team will get together to have their Daily Standup.
5. **Showcase** – At the end of the Sprint, the team will organise a Showcase session, where the completed work is demoed to key stakeholders and feedback is captured.
6. **Sprint Planning & Retrospectives** – Following the showcase, the team will get together to have the next sprint planning session. Any feedback will be included in the backlog and the next sprint will be agreed. If necessary, a sprint Retrospective will take place.
7. **Repeat** – The next sprint starts and we repeat from step 3 onwards.

