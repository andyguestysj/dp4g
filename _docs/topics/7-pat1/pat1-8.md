---
title: Observer Pattern
permalink: /docs/pat1-8/
---

Rather than pointlessly copying and pasting all the text from [https://gameprogrammingpatterns.com/](https://gameprogrammingpatterns.com/) I'll just put the Python versions of the code from that site here.  

The observer method is a **Behavioral Design Pattern** which allows you to define or create a subscription mechanism to send the notification to the multiple objects about any new event that happens to the object that they are observing. The subject is basically observed by multiple objects. The subject needs to be monitored and whenever there is a change in the subject, the observers are being notified about the change. This pattern defines one to Many dependencies between objects so that one object changes state, all of its dependents are notified and updated automatically.  

## [Game Programming Patterns - Observer Pattern](https://gameprogrammingpatterns.com/observer.html)

![Observer pattern diagram](/assets/img/pat1/Observer.png "Observer pattern diagram")    

[Code in replit](https://replit.com/@andyguest/pyObserver)  
[Originally from https://www.geeksforgeeks.org/observer-method-python-design-patterns/](https://www.geeksforgeeks.org/observer-method-python-design-patterns/) so is not a perfect match for the Game Patterns books  

```python
class Subject: 
  
    """Represents what is being observed"""
  
    def __init__(self): 
  
        """create an empty observer list"""
  
        self._observers = [] 
  
    def notify(self, modifier = None): 
  
        """Alert the observers"""
  
        for observer in self._observers: 
            if modifier != observer: 
                observer.update(self) 
  
    def attach(self, observer): 
  
        """If the observer is not in the list, 
        append it into the list"""
  
        if observer not in self._observers: 
            self._observers.append(observer) 
  
    def detach(self, observer): 
  
        """Remove the observer from the observer list"""
  
        try: 
            self._observers.remove(observer) 
        except ValueError: 
            pass
  
  
  
class Data(Subject): 
  
    """monitor the object"""
  
    def __init__(self, name =''): 
        Subject.__init__(self) 
        self.name = name 
        self._data = 0
  
    @property
    def data(self): 
        return self._data 
  
    @data.setter 
    def data(self, value): 
        self._data = value 
        self.notify() 
  
  
class HexViewer: 
  
    """updates the Hewviewer"""
  
    def update(self, subject): 
        print('HexViewer: Subject {} has data 0x{:x}'.format(subject.name, subject.data)) 
  
class OctalViewer: 
  
    """updates the Octal viewer"""
  
    def update(self, subject): 
        print('OctalViewer: Subject' + str(subject.name) + 'has data '+str(oct(subject.data))) 
  
  
class DecimalViewer: 
  
    """updates the Decimal viewer"""
  
    def update(self, subject): 
        print('DecimalViewer: Subject % s has data % d' % (subject.name, subject.data)) 
  
"""main function"""
  
if __name__ == "__main__": 
  
    """provide the data"""
  
    obj1 = Data('Data 1') 
    obj2 = Data('Data 2') 
  
    view1 = DecimalViewer() 
    view2 = HexViewer() 
    view3 = OctalViewer() 
  
    obj1.attach(view1) 
    obj1.attach(view2) 
    obj1.attach(view3) 
  
    obj2.attach(view1) 
    obj2.attach(view2) 
    obj2.attach(view3) 
  
    obj1.data = 10
    obj2.data = 15
```

