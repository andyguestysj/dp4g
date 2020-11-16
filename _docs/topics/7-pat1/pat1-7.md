---
title: Event Queue
permalink: /docs/pat1-7/
---

Rather than pointlessly copying and pasting all the text from [https://gameprogrammingpatterns.com/](https://gameprogrammingpatterns.com/) I'll just put the Python versions of the code from that site here.  

## [Game Programming Patterns - Event Queue Pattern](https://gameprogrammingpatterns.com/event-queue.html)

A **queue** stores a series of **notifications or requests** in first-in, first-out order. Sending a notification **enqueues the request and returns**. The request processor then **processes items from the queue** at a later time. Requests can be **handled directly** or **routed to interested parties**. This **decouples the sender from the receiver** both **statically** and in **time**.

```python
class PlayMessage:
  def __init__(self, ID, volume):
    self.id_ = ID
    self.volume_ = volume


class Audio:
  MAX_PENDING = 16
  
  def __init__(self):    
    self.pending_ = []
    self.head_ = 0
    self.tail_ = 0

  def playSound(self, ID, volume):
    for i in range(self.head_, self.tail_,1):
      if i>=self.MAX_PENDING:
        i = 0

      if self.pending_[i].id_ == ID:
        self.pending_[i].volume_ = max(self.pending_[i].volume_, volume)
        return

    if (self.tail+1) % self.MAX_PENDING != self.head_:
      self.pending_.append(PlayMessage(ID,volume))  
      self.tail_ = (self.tail_) % self.MAX_PENDING
  
  def update(self):
    if (self.head_==self.tail_):
      return
    

      # LoadSound(self.pending_[self.head_}.id_)
      # GetOpenChannel or return
      # startSound()
      pass
    
    self.head_ = (self.head_) % self.MAX_PENDING
```