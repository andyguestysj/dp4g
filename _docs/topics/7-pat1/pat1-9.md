---
title: Prototype Pattern
permalink: /docs/pat1-9/
---

Rather than pointlessly copying and pasting all the text from [https://gameprogrammingpatterns.com/](https://gameprogrammingpatterns.com/) I'll just put the Python versions of the code from that site here.  

## [Game Programming Patterns - Prototype Pattern](https://gameprogrammingpatterns.com/prototype.html)

[Code in replit](https://replit.com/@andyguest/pyPrototypeGPP)  


```python
class Monster:
  def __init__(self):
    pass
  def clone(self):
    pass


class Ghost(Monster):

  def __init__(self, health, speed):
    self.health_ = health
    self.speed = speed

  def clone(self):
    return Ghost(self.health, self.speed)

class Demon(Monster):

  def __init__(self, health, speed):
    self.health_ = health
    self.speed = speed

  def clone(self):
    return Demon(self.health, self.speed)


class Spawner:
  def __init__(self, prototype):
    self.prototype_ = prototype

  def spawnMonster(self):
    return self.prototype_.clone()
```

```python
# main.py
ghostPrototype = Ghost(15,3)
ghostSpawner = Spawner(ghostPrototype)

demonSpawner = Spawner(Demon(20,6))


print (ghostSpawner.prototype_.speed)
```

There is another version of the Prototype pattern at [Geeks for Geeks](https://www.geeksforgeeks.org/prototype-method-python-design-patterns/)  

