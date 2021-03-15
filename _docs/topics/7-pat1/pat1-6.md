---
title: Object Pool Pattern
permalink: /docs/pat1-6/
---

Rather than pointlessly copying and pasting all the text from [https://gameprogrammingpatterns.com/](https://gameprogrammingpatterns.com/) I'll just put the Python versions of the code from that site here.  

## [Game Programming Patterns - Object Pool Pattern](https://gameprogrammingpatterns.com/object-pool.html)

The Object Pool pattern improves performance and memory use by reusing objects from a pool rather than constantly creating and deleting them.  

A simple implementation is shown below. It iterates over a list of pre-created objects and animates those that are `inUse`. When a 'new' object is required one of the objects that is not `inUse` is used rather than creating a new one. When an object is no longer required it is set so it is not `inUse` rather than deleted.  

```python
class Particle:
  def __init__(self):
    self.x_ = 0
    self.y_ = 0
    self.xVel_ = 0
    self.yVel_ = 0
    self.framesLeft_ = 0

  def init(self, x, y, xVel, yVel, lifetime):
    self.x_ = x
    self.y_ = y
    self.xVel_ = xVel
    self.yVel_ = yVel
    self.framesLeft_ = lifetime;

  def animate(self):
    if not self.inUse():
      return

    self.framesLeft_ -= 1
    self.x_ += self.xVel_;
    self.y_ += self.yVel_;


  def inUse(self):
    if self.framesLeft_ > 0:
      return True
    else:
      return False

class ParticlePool:
  POOL_SIZE = 100

  def __init__(self):
    self.particles_ = []
    for i in range(self.POOL_SIZE):
      self.particle.append(Particle())

  def create(self,x, y, xVel, yVel, lifetime):
    for particle in self.particles_:    
      if not particle.inUse():
        particle.init(x, y, xVel, yVel, lifetime)

  def animate(self):
    for particle in self.particles_:    
      particle.animate();
```

This could still be more efficient. 100 particles are created at the start, if only fifty are ever used at a time we are wasting memory and processing power. Additionally we have to iterated through every particle when animating, accessing the unused ones only to discover we don't need to do anything with them.  

Code at [https://replit.com/@andyguest/pyObjectPool](https://replit.com/@andyguest/pyObjectPool)

## More Efficient Version

If we instead store two lists, a list of `used` particles and another list of `unused` particles then we  can can improve our efficiency. When we `animate` we only animate the used particles. When we require a new particle we can move one from the `unused` list to the `used` list. When we no longer require a particle we move it from the `used` list to the `unused` one.  

For extra efficiency we don't create every possible particle at the start. Instead when we want a new particle we first check if the pool is full. If the pool isn't full we check to see if there are any particles in the `unused` list. If there is we move one from the `unused` list to the `used` list and that is out new particle. If the `unused` list is empty (and we have space in the pool) we create a new particle and add it to the used list.  

This approach means we never create new particles unless we need more than are currently available. We won't create 100 particles when we never need more than 50 at a time. There *will* still be times when we have more particles than we need, that's the cost to the object pool.  

The object pool pattern should improve performance if the number of active objects varies or if you are regularly creating and deleting objects. 

Code at [https://replit.com/@andyguest/pyObjectPool2](https://replit.com/@andyguest/pyObjectPool2)

```python
import random

class Particle:
  def __init__(self):
    self.x_ = 0
    self.y_ = 0
    self.xVel_ = 0
    self.yVel_ = 0
    self.framesLeft_ = 0

  def init(self, x, y, xVel, yVel, lifetime):
    self.x_ = x
    self.y_ = y
    self.xVel_ = xVel
    self.yVel_ = yVel
    self.framesLeft_ = lifetime;

  def animate(self):
    # should never happen now
    if not self.inUse():
      return

    self.framesLeft_ -= 1
    self.x_ += self.xVel_;
    self.y_ += self.yVel_;

  def inUse(self):
    if self.framesLeft_ > 0:
      return True
    else:
      return False

class ParticlePool:
  POOL_SIZE = 100
  _unused = list()
  _used = list()

  def __init__(self):
    pass

  def create(self,x, y, xVel, yVel, lifetime):
    # if we have unused particles use one of them
    if len(self._unused)>0:
      # grab an unused particle and remove it from the unused list
      newParticle = self._unused.pop()
      # set the particles values
      newParticle.init(x, y, xVel, yVel, lifetime)
      # add the particle to the used list
      self._used.append(newParticle)
    elif len(self._used)< self.POOL_SIZE:
      # no available unused particles but pool not full, so add new particle to used 
      newParticle = Particle()
      newParticle.init(x, y, xVel, yVel, lifetime)
      self._used.append(newParticle)
    else:
      # pool full, can't create new
      return None

  
  def animate(self):
    for particle in self._used:    
      particle.animate()
      # check if particle is still inUse
      if not particle.inUse():
        # add particle to _unused to be used again
        self._unused.append(particle)
        # remove from used list
        self._used.remove(particle)


def newParticle(aPool):
  x = random.randint(20,25)
  y = 0
  xVel = random.randint(-5,5)
  yVel = random.randint(0,5)
  life = random.randint(15,20)
  aPool.create(x,y,xVel,yVel,life) 

myPool = ParticlePool()
for i in range(50):
  newParticle(myPool)



timer = 100

while timer>0:
  timer -= 1
  myPool.animate()
  poolCount = len(myPool._used)
  if poolCount<20:
    for i in range(50-poolCount):
      newParticle(myPool)
  print("pool count",poolCount)
```