---
title: Double Buffer Pattern
permalink: /docs/pat1-4/
---

Rather than pointlessly copying and pasting all the text from [https://gameprogrammingpatterns.com/](https://gameprogrammingpatterns.com/) I'll just put the Python versions of the code from that site here.  

## [Game Programming Patterns - Double Buffer](https://gameprogrammingpatterns.com/double-buffer.html)

### Framebuffer Code

[Framebuffer example in replit.com](https://replit.com/@andyguest/pyDoubleBufferFrames#main.py)

**framebuffer.py**
```python
import numpy as np

class Framebuffer:

    WIDTH = 5
    HEIGHT = 5

    # Create a 1D array with WIDTH*HEIGHT entries

    def clear(self):
      for i in range(0,self.WIDTH*self.HEIGHT):
        self.pixels_[i] = 0

    def draw(self, point):
      self.pixels_[(self.WIDTH*point[1])+point[0]] = 1

    def show(self):
      B = np.reshape(self.pixels_, (-1, self.WIDTH))

      for row in B:
        print (row)

    def __init__(self,index):
        self.pixels_ = [0]*(self.WIDTH*self.HEIGHT)
        self.clear()
        self.index = index
```

**scene.py**
```python
from framebuffer import Framebuffer

class Scene:
  
  def __init__(self):
    self.buffers_ = []    
    self.buffers_.append(Framebuffer(1))
    self.buffers_.append(Framebuffer(2))
    self.current_ = self.buffers_[0]
    self.next_ = self.buffers_[1]

    self.current_.clear()
    self.next_.clear()

  def swap(self):
      temp = self.current_
      self.current_ = self.next_
      self.next_ = temp      

  def draw(self,points):
    self.next_.clear()
    
    for point in points:
      self.next_.draw(point)
    self.swap()

  def show(self, buf = "current"):
    if buf=="current":
      print("Current Buffer")
      self.current_.show()
    elif buf=="next":
      print("Next Buffer")
      self.next_.show()
    else:
      print("Current Buffer")
      self.current_.show()
      print("Next Buffer")
      self.next_.show()
```

**main.py**
```python
from scene import Scene

myScene = Scene()

myScene.draw([[0,1],[3,1],[0,3],[1,4],[2,4],[3,3]])

myScene.show("both")

myScene.draw([[1,1],[4,1],[1,3],[2,4],[3,4],[4,3]])

myScene.show("both")
```

### Actors Code

[actors example in replit.com](https://replit.com/@andyguest/pyDoubleBufferActors)

**actor.py**
```python
class Actor:

  def update(self):
    pass
  
  def reset(self):
    self.slapped_ = False

  def swap(self):
    self.currentSlapped_ = self.nextSlapped_
    self.nextSlapped_ = False

  def slap(self):
    self.nextSlapped_ = True

  def wasSlapped(self):
    return self.currentSlapped_

  def __init__(self,name):
    self.currentSlapped_ = False
    self.nextSlapped_ = False
    self.name_ = name

class Comedian(Actor):

  def update(self):
    print("Stage updates", self.name_)
    if self.wasSlapped():
      self.facing_.slap()
      print("  ", self.name_, "was slapped, so slaps", self.facing_.name_)
    else:
      print("  ", self.name_, "was not slapped so does nothing")

  def face(self, actor):
    self.facing_ = actor


  def __init__(self,name):
    super().__init__(name)
```

**stage.py**
```python
class Stage:
  def add(self, actor, index):
    self.actors_.append(actor)

  def update(self):
    for actor in self.actors_:
      actor.update()
    for actor in self.actors_:
      actor.swap()

  def __init__(self):
    self.NUM_ACTORS = 3
    self.actors_=[]

  def ListActors(self):
    for actor in self.actors_:
      print(actor.name_)
```

**main.py**
```python
from stage import Stage
from actor import Comedian

stage = Stage()

harry = Comedian("harry")
baldy = Comedian("baldy")
chump = Comedian("chump")



harry.face(baldy)
baldy.face(chump)
chump.face(harry)

stage.add(harry,0)
stage.add(baldy,1)
stage.add(chump,2)

harry.slap()

print("==============")
print("Update 1")
stage.update()
print("==============")
print("Update 2")
stage.update()
print("==============")
print("Update 3")
stage.update()
print("==============")
print("Update 4")
stage.update()
```

