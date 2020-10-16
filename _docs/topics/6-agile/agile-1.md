---
title: Product Backlog
permalink: /docs/agile-1/
---

A product backlog is a prioritized list of work for the development team that is derived from the roadmap and its requirements. The most important items are shown at the top of the product backlog so the team knows what to deliver first.  

The **Product Backlog** is a decision-making artifact that helps you estimate, refine, and prioritize everything you might sometime in the future want to complete.  It helps ensure the team is working on the most important and valuable features, fixing the most important bugs, or doing other important work critical to product development.  

The backlog, therefore, is tremendously useful in situations when you are unable to do everything being asked (so, most situations), or in contexts when even a small amount of planning will help a lot (so, in most contexts).  

Many think of this backlog as a to-do list, and define it in exactly this way, as a list of things you must do to deliver your product to market. In truth, it is not necessarily a to-do list. Think of it as a wish list.  

## Backlog Item Categories

Four main categories of items (called product backlog items) fit in the product backlog. Two are highly visible to customers — features and bugs. The other two, technical debt and research, are invisible to customers yet can't be ignored.  

In an Agile organization, product backlog items are typically written as user stories — though they don’t always need to be. They can also be written as traditional requirements documents, or in a number of other ways.  

When written as user stories, product backlog items often take the following form:

>As a <**stakeholder**>, I want <**action**> so that <**benefit**>.

### New Features

Requests for new features originate from a multitude of sources. These include end users, sales, support, product management, and so on. New features can be the most difficult to prioritize as you try to balance the competing needs of:
* Keeping existing customers satisfied.
* Meeting near-term sales opportunities.
* Working toward a longer-term vision of your product.
The product owner should monitor these sources routinely and resolve any conflicting requests. Doing so will help make sure the backlog contains new features that both attract new customers and build loyalty with existing ones.  

> As a <**new feature**>, I want <**to be understood and prioritized appropriately**> so that <**I can deliver maximum value to customers and owners**>.  

### Technical Debt
Technical debt includes work that needs to be done for the product to stay up to date and be maintainable. Examples of PBIs to address technical debt include upgrading to the latest third-party libraries, making architectural changes to support better scalability, or refactoring the source code to prevent future maintenance issues. When technical debt builds up – whether deliberately or unknowingly — you can risk delaying product releases.  

Technical debt is often the result of change regarding:
* Direction and scope.
* Performance and scalability expectations.
* Technology or best practices.

These types of PBIs are often referred to as ”technical debt” because of their similarity to financial debt; you will have to pay interest for them, but in the form of a longer development lifecycle. These tasks should be added to the backlog, and then prioritized along with features and defects, so they can be included in the planning cycle.

>As <**technical debt**>, I want <**to be understood and prioritized appropriately**> so that <**we can maintain and improve the product without delay**>.  

### Bugs
Bugs and defects are problems discovered by end users that escaped quality control during development. In a Waterfall process, testing is often the last step of the development lifecycle. It’s quite common to push a release live with a large collection of minor (and sometimes moderate) defects. Bugs tend to cluster and accumulate over time if they aren’t resolved. They are sometimes managed within an issue tracker, but can also be included as a part of the backlog.  

>As a <**bug**>, I want <**to be understood and prioritized appropriately**> so that <**problems are addressed early and the product is high quality**>.  

### Research
Research is another item the end user won’t recognize as a feature, but can be included in a backlog. Research is instrumental when you know very little about how to implement a new feature or concept, or want to try something new. Either way, circumstances require you set aside time to expand the team’s understanding. The output of these user stories, commonly called “spikes”, is not working code, but knowledge.  

>As <**research**>, I want <**to be understood and prioritized appropriately**> so that <**we can lower business risk and innovate**>.  

## Creating A Product Backlog
1. Add ideas to the backlog
Stakeholders will typically be approaching you with ideas for product improvements
2. Get clarification
Once you’re approached by a stakeholder with a product addition or fix, make sure you understand:
* The reason behind the addition or fix
* The amount of value it contributes to the product as a whole
* The specifications of the item
3. Prioritize
The backlog should have clearly defined, high-priority items at the top and vague items that are not a priority at the bottom. If an item has no value, it should not be added to the backlog. 
4. Update the backlog regularly
The backlog is a living document; make sure you’re constantly prioritizing, refining, and keeping the backlog up to date.  

You may have hundreds of items in your backlog as ideas for product improvements are suggested. Some of these items may be discarded, but many of them will begin making their way up the backlog for further refinement and, ultimately, development.

### Product Backlog Prioritization
The product backlog itself is owned by the product owner. The product owner’s job is to produce the very best product possible, so that means developing the most valuable additions to the software first. Since the product backlog is ranked in order of most valuable components, it would stand to reason that the most valuable addition would be at the very top. But that’s not necessarily the case, as the most valuable addition likely has dependencies that need to be developed first.  

* **Higher-priority** items should be refined and have great value to the product.
* **Mid-priority** items should be candidates for refinement (the process of detailing each task)
* **Low-priority** items should not be a dependency and can be safely ignored until they are candidates for refinement.

As items progress closer to the top of the list to be added to the next sprint cycle, they should be refined so they can be better acted upon. Here’s a helpful tip: colour-code each block to indicate an item is sufficiently refined and ready for sprint planning by colouring it green. You may wish to indicate mid-priority items with yellow and low-priority items with red. Or go crazy and make everything neon.  

### Product Refinement
Product refinement is the process of refining the tasks in the product backlog so that they’re clear enough to be action items instead of nebulous ideas.  

Say your team is developing a dating app. One of the requests from stakeholders and customers has been to have an integrated background checker, so you add that to the product backlog. However, that’s not nearly defined enough to start assigning tasks for developing the background checker.  

Add necessary details right in each task of the product backlog so there’s never any confusion about what each item is. For instance, with our dating app background checker, you can easily detail what kind of agency you’ll be pairing with to provide a background check, what information should be gathered from the user to perform the background check, and what the ultimate goal of the background check should be. You can also easily add links, pictures, or any other information.  

There are two schools of thought with product refinement: Some teams prefer to refine all the items in a product backlog while others prefer to “groom as you go,” refining mid-priority items so they can be elevated to high-priority items.  

## Sprint Planning
A scrum product backlog ultimately makes sprint planning much easier. After all, your to-do items are already defined for you in the backlog, and they can be easily moved onto your scrum board. Using each item’s estimation allows you to determine how many action items can be added to the next sprint. Then it’s a matter of following the sprint cycle guidelines to follow each item through to completion. 
