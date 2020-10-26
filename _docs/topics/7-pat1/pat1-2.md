---
title: Update Method
permalink: /docs/pat1-2/
---

## Intent

*Simulate a collection of independent objects by telling each to process one frame of behavior at a time.*

## Motivation

The player’s mighty valkyrie is on a quest to steal glorious jewels from where they rest on the bones of the long-dead sorcerer-king. She tentatively approaches the entrance of his magnificent crypt and is attacked by… nothing. No cursed statues shooting lightning at her. No undead warriors patrolling the entrance. She just walks right in and grabs the loot. Game over. You win.  

Well, that won’t do.  

This crypt needs some guards — enemies our brave heroine can grapple with. First up, we want a re-animated skeleton warrior to patrol back and forth in front of the door. If you ignore everything you probably already know about game programming, the simplest possible code to make that skeleton lurch back and forth is something like:  

>If the sorcerer-king wanted more intelligent behavior, he should have re-animated something that still had brain tissue.  

```python
while true
{
  // Patrol right.
  for x in range(0, 100, 1)
    skeleton.setX(x)

  // Patrol left.
  for x in range(100, 1, -1)
    skeleton.setX(x)
```

## The Pattern


## When To Use It


## Keep In Mind


## Sample Code


## Design Decisions