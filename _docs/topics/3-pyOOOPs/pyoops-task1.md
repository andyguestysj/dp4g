---
title: Python OOPs Exercises
permalink: /docs/pyoops-task1/
---
#### Exercise 1 

1. Clone the repository [https://replit.com/@andyguest/pyFirstClass](https://replit.com/@andyguest/pyFirstClass) and open it.
2. Work your way through the tasks in the code - they are in the comments

#### Exercise 2 
1. Give the JackRusselTerrier a method called "is_scrappy()" that returns a string describing how the dog behaves around others
2. Give the subclass you created a method no other class has that describes a unique feature of your dog
3. Create a new mutant dog class that inherits from both your dog class and JackRusselTerrier
4. Create an object of this new class
5. Verify that you can call both the scrappy() method and your new method on the mutant dog

#### Exercise 3
1. Return to pyFirstClass
2. Override the addition operator on the `Dog` class so that you can create a new dog object with the code below
```python
fred = Dog("Fred",5)
wilma = Dog("Wilma",4)
pebbles = fred + wilma
```
The new dog's name should be set to "Child of Fred and Wilma" and its age should be set to 0.
