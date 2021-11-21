---
title: Observer Pattern
permalink: /docs/pattern-2/
---

### Observer Pattern

The observer method is a **Behavioral Design Pattern** which allows you to define or create a subscription mechanism to send the notification to the multiple objects about any new event that happens to the object that they are observing. The subject is basically observed by multiple objects. The subject needs to be monitored and whenever there is a change in the subject, the observers are being notified about the change. This pattern defines One to Many dependencies between objects so that one object changes state, all of its dependents are notified and updated automatically.  

![Observer pattern diagram](/assets/img/pat1/Observer.png "Observer pattern diagram")    

#### When To Use The Observer Pattern

When we have a design a system where multiple entities are interested in any possible update to some particular second entity object, we can use the observer pattern.  
![Observer pattern example](/assets/img/pat1/observer-pattern.png "Observer pattern example")    

The flow is very simple to understand. Application creates the concrete subject object. All concrete observers register themselves to be notified for any further update in the state of subject.  

As soon as the state of subject changes, subject notifies all the registered observers and the observers can access the updated state and act accordingly.  
![Observer pattern sequence](/assets/img/pat1/observer_pattern_seq.png "Observer pattern sequence")    

#### Real World Example

A real world example of observer pattern can be any social media platform such as Facebook or twitter. When a person updates his status – all his followers gets the notification.  
A follower can follow or unfollow another person at any point of time. Once unfollowed, person will not get the notifications from subject in future.  

#### Architecture
![Observer pattern architecture](/assets/img/pat1/observer-pattern-arch.jpg "Observer pattern architecture")    

* **Subject** – interface or abstract class defining the operations for attaching and de-attaching observers to the subject.
* **ConcreteSubject** – concrete Subject class. It maintain the state of the object and when a change in the state occurs it notifies the attached Observers.
* **Observer** – interface or abstract class defining the operations to be used to notify this object.
* **ConcreteObserver** – concrete Observer implementations.

#### Code Example

**Subject**

```java
public interface Subject 
{
    public void attach(Observer o);
    public void detach(Observer o);
    public void notifyUpdate(Message m);
}
```

**ConcreteSubject**

```java
import java.util.ArrayList;
import java.util.List;
 
public class MessagePublisher implements Subject {
     
    private List<Observer> observers = new ArrayList<>();
 
    @Override
    public void attach(Observer o) {
        observers.add(o);
    }
 
    @Override
    public void detach(Observer o) {
        observers.remove(o);
    }
 
    @Override
    public void notifyUpdate(Message m) {
        for(Observer o: observers) {
            o.update(m);
        }
    }
}
```

**Observer**

```java
public interface Observer 
{
    public void update(Message m);
}
```

**ConcreteObserver**

```java
public class MessageSubscriberOne implements Observer 
{
    @Override
    public void update(Message m) {
        System.out.println("MessageSubscriberOne :: " + m.getMessageContent());
    }
}

public class MessageSubscriberTwo implements Observer 
{
    @Override
    public void update(Message m) {
        System.out.println("MessageSubscriberTwo :: " + m.getMessageContent());
    }
}

public class MessageSubscriberThree implements Observer 
{
    @Override
    public void update(Message m) {
        System.out.println("MessageSubscriberThree :: " + m.getMessageContent());
    }
}
```

**State Object**

This must be an immutable object so that no class can modify it’s content by mistake.

```java
public class Message 
{
    final String messageContent;
     
    public Message (String m) {
        this.messageContent = m;
    }
 
    public String getMessageContent() {
        return messageContent;
    }
}
```

Now test the communication between publisher and subscribers.

```java
public class Main 
{
    public static void main(String[] args) 
    {
        MessageSubscriberOne s1 = new MessageSubscriberOne();
        MessageSubscriberTwo s2 = new MessageSubscriberTwo();
        MessageSubscriberThree s3 = new MessageSubscriberThree();
         
        MessagePublisher p = new MessagePublisher();
         
        p.attach(s1);
        p.attach(s2);
         
        p.notifyUpdate(new Message("First Message"));   //s1 and s2 will receive the update
         
        p.detach(s1);
        p.attach(s3);
         
        p.notifyUpdate(new Message("Second Message")); //s2 and s3 will receive the update
    }
}
```

#### FAQs

* **Can different types of observers register to one subject?**
The nature and functionality of observers can be different but they all must implement the one common Observer interface which the subject support for registering and deregistering.
* **Can I add or remove observers at runtime?**
Yes. We can add or remove the observers at any point of time.
* **Difference between observer pattern and chain of responsibility pattern?**
In an observer pattern, all registered handler objects get notifications at the same time and they process the update at same time.  
But in a chain of responsibility pattern, handler objects in the chain are notified one by one, and this process continues until one object fully handles the notification.  
* **Benefits of the observer pattern?**
The subject and observers make a loosely coupled system. They do not need to know each other explicitly. We can independently add or remove observers at any time.

**Collated from**  
* [howtodoitinjava](https://howtodoinjava.com/design-patterns/behavioral/observer-design-pattern/)
* [GeeksForGeeks](https://www.geeksforgeeks.org/observer-pattern-set-1-introduction/?ref=lbp)  
* [tutorialspoint.com](https://www.tutorialspoint.com/design_pattern/observer_pattern.htm)
* [Wikipedia](https://en.wikipedia.org/wiki/Observer_pattern)
* [Game Programming Patterns](https://gameprogrammingpatterns.com/observer.html)