---
title: State Pattern
permalink: /docs/pat1-5/
---

Rather than pointlessly copying and pasting all the text from [https://gameprogrammingpatterns.com/](https://gameprogrammingpatterns.com/) I'll just put the Python versions of the code from that site here.  

## [Game Programming Patterns - State Pattern](https://gameprogrammingpatterns.com/state.html)

Code at [https://repl.it/@andyguest/pyStatePattern1](https://repl.it/@andyguest/pyStatePattern1)

### Enum

Enum's in Python can be made using the `Enum` class from `enum`. [enum](https://docs.python.org/3/library/enum.html)  

```python
from enum import Enum, auto

class State(Enum):
  STATE_STANDING = auto()
  STATE_JUMPING = auto()
  STATE_DUCKING = auto()
  STATE_DIVING = auto()
```

We have to ensure each enum has a value. We can assign them manually but if what don't care what the value is we can use `auto()` to assign it for us.  

### Heroine handleInput

Python doesn't have a direct equivalent of a `switch` statement so we have to use `if, elif, else` instead.  

```python
class Heroine:
  JUMP_VELOCITY = 5

  def __init__(self):
    self.state_ = State.STATE_STANDING

  def handleInput(self, input):

    if self.state_== State.STATE_STANDING:
      if input == PRESS_B:
        self.state_ = self.STATE_JUMPING
        yVelocity_ = self.JUMP_VELOCITY
        self.setGraphics(IMAGE_JUMP)
      elif input == PRESS_DOWN:
        self.state_ = self.STATE_DUCKING;
        self.setGraphics(IMAGE_DUCK);
    elif self.state == State.STATE_JUMPING:
      if input == PRESS_DOWN:
        self.state_ = self.STATE_DIVING
        self.setGraphics(IMAGE_DIVE)
    elif self.state == State.STATE_DUCKING:
      if input == RELEASE_DOWN:
        self.state_ = self.STATE_STANDING
        self.setGraphics(IMAGE_STAND)
```

## Heropine State Pattern 

Code at [https://repl.it/@andyguest/pyStatePattern2](https://repl.it/@andyguest/pyStatePattern2)