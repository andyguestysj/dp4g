---
title: Branching & Looping
permalink: /docs/py-3/
---

## `if` Statements
```python
if x < 0:
    x = 0 # negatives not allowed
    print('zero')
elif x == 0:
    print('zero')
elif x == 1:
    print('single')
else:
    print('more')  
```

## `for` in Python

`for` in Python is very versatile. It is used for iterating over a sequence and in Python there are many types of sequence.  

### The `range()` Function

We are used to iteration over a range over numbers. In Java we might use a loop like  
```java
for (int i=0; i<10; i++)
{
    System.outlput.println(i);
}
```
to loop through the integers from zero to nine.

In Python we can use the `range()` function to generate a sequence of numbers which can then be used in a `for` statement.  

`range(*optional* start_value, end_value, *optional* step_size)`

```python
range(1,5) # generates a sequence from 1 to 5 (but not including 5) - 1,2,3,4
range(2,12,2) # generates a sequence from 2 to 10, increasing by 2 each time - 2,4,6,8,10
range(4,-1,-1) # generates a sequence from 4 to 0, decreasing by 1 each time - 4,3,2,1,0
range(3) # generates a sequence from 0 to 2 - 0, 1, 2
```

`range(*optional* start_value, end_value, *optional* step_size)` generates a sequence from `start_value` to `end_value` (but doesn't include `end_value`) with each step changing by `step_size`.  If only one argument is given to `range(x)` the sequence runs from 0 to x, not including x, increasing by one each time. Two arguments `range(x,y)` generates a sequence from x to y (not including y), increasing by 1. Three arguments `range(x,y,z)` from x to y (not including y), increasing by z each time.

### `for` using `range`

```python
for i in range(10,20):
    print(i)
for j in range(6):
    print(j)
```

### `for` and `else`
```python
for x in range(6):
  print(x)
else:
  print("Finally finished!")
```
The code after the `else` will be executed when the code is completed.  

```python
sum = 0
for x in range(6):
  sum = sum + x
else:
  print("Sum is " + sum)
```

### Nested Loops

For loops can be nested as you would expect.  
```python
for x in range(6):
  for y in range(6):
    print(x,y)
```
### Other Sequences

Any list, tuple, set, etc. can be used in a for loop.  

```python
days = ["sat", "sun", "mon", "tue", "wed", "thu", "fri"]
for day in days:
    print(day)
```

Given a string a for can loop through the characters in the string.  
```python
a_string = "Hello Mum"
for character in a_string:
    print(character)
```

### `break` in loops
```python
days = ["sat", "sun", "mon", "tue", "wed", "thu", "fri"]
for day in days:    
    if day == "tue":
      break
    print(day)
```
will exit when `day` reaches `tue` without printing it out.  

### `continue` in loops
```python
days = ["sat", "sun", "mon", "tue", "wed", "thu", "fri"]
for day in days:    
    if day == "tue":
      continue
    print(day)
```
With the `continue` statement we can stop the current iteration of the loop, and continue with the next.  


