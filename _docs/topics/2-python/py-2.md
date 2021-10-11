---
title: Python Specifics
permalink: /docs/py-2/
---

The features on this page are significantly different from the way Java works.  

## Lists

Python lists are extremely versatile and useful. A list contains items separated by commas and enclosed within square brackets. Every item in a list can be of a different type, including another list.

```python
list = [ 'abcd', 786 , 2.23, 'john', 70.2 ]
tinylist = [123, 'john']
listinlist = [["hello", 24], 1.2, 'a', 321]
listsofdifferentsizes = [[1,2],["Hello", "Mother", "Hello", "Father"],[1,2,3,4,5,6],[1,[1,2]]]
```

The values stored in a list can be accessed using the slice operator ([ ] and [:]) with indexes starting at 0 in the beginning of the list and working their way to (length -1). The plus (+) sign is the list concatenation operator, and the asterisk (*) is the repetition operator. For example −

```python
print list          # Prints complete list
print list[0]       # Prints first element of the list
print list[1:3]     # Prints elements starting from 2nd till 3rd 
print list[2:]      # Prints elements starting from 3rd element
print tinylist * 2  # Prints list two times
print list + tinylist # Prints concatenated lists
print (list[-2:-1]) # Prints elements starting from the second last to the last, negative indexes
```
```console
['abcd', 786, 2.23, 'john', 70.2]
abcd
[786, 2.23]
[2.23, 'john', 70.2]
[123, 'john', 123, 'john']
['abcd', 786, 2.23, 'john', 70.2, 123, 'john']
```

### Changing An Entry
```python
list = ['abcd', 786, 2.23, 'john', 70.2, 123, 'john']
list[1] = 1
# list is now ['abcd', 1, 2.23, 'john', 70.2, 123, 'john']
```

### List Size
You can get the number of elements in a list using `len()`.  

```python
list = [123, 'john', 123, 'john']
print(len(list))
```

### Sorting a List

```python
list.sort()
```

### Adding to a list
```python
list = [123, 'john', 123, 'john']
list.append(21)
```

### Removing from a list
#### `remove()`
```python
list = [123, 'john', 123, 'john']
list.remove('john')
# list is now [123, 123]
```
`remove()` deletes the first matching entry.  

#### `pop()`
```python
list = [123, 'john', 123, 'john']
list.pop(2)
# list is now [123, 'john', 'john']
```
`pop()` removes the item with the specified index.  

#### `clear()`
```python
list = [123, 'john', 123, 'john']
list.clear()
# list is now []
```
`clear()` deletes the list

### Copying Lists
You cannot simply use `list2 = list1`, this will result in both being references to the same list. To make a copy of a list you can use the `copy()` function.  
```python
list1=[1,2,34,4,76]
list2 = list1.copy()
```

### Concatenating Lists
```python
list1 = ["a", "b" , "c"]
list2 = [1, 2, 3]

list3 = list1 + list2

list4 = list1.copy()
for x in list2:
    list4.append(x)
```


### Check is something is in the list
```python
list = [123, 'john', 123, 'john']
if "john" in list:
    print("found")
```

## Tuples

 A tuple is another sequence data type that is similar to the list. A tuple consists of a number of values separated by commas. Unlike lists, however, tuples are enclosed within parentheses.  

The main differences between lists and tuples are: Lists are enclosed in brackets ([]) and their elements and size can be changed, while tuples are enclosed in parentheses (()) and cannot be updated. Tuples can be thought of as read-only lists. Because they are read-only tuples are faster to access. For example −   

```python
tuple = ( 'abcd', 786 , 2.23, 'john', 70.2  )
tinytuple = (123, 'john')

print tuple               # Prints the complete tuple
print tuple[0]            # Prints first element of the tuple
print tuple[1:3]          # Prints elements of the tuple starting from 2nd till 3rd 
print tuple[2:]           # Prints elements of the tuple starting from 3rd element
print tinytuple * 2       # Prints the contents of the tuple twice
print tuple + tinytuple   # Prints concatenated tuples
```
Produces  
```console
('abcd', 786, 2.23, 'john', 70.2)
abcd
(786, 2.23)
(2.23, 'john', 70.2)
(123, 'john', 123, 'john')
('abcd', 786, 2.23, 'john', 70.2, 123, 'john')
```

## Dictionary
Python's dictionaries are kind of hash table type. They work like associative arrays or hashes found in Perl and consist of key-value pairs. A dictionary key can be almost any Python type, but are usually numbers or strings. Values, on the other hand, can be any arbitrary Python object.  

Dictionaries are enclosed by curly braces ({}) and values can be assigned and accessed using square braces ([]).  

```python
dict = {}
dict['one'] = "This is one"
dict[2]     = "This is two"

tinydict = {'name': 'john','code':6734, 'dept': 'sales'}


print (dict['one'])       # Prints value for 'one' key
print (dict[2])           # Prints value for 2 key
print (tinydict)          # Prints complete dictionary
print (tinydict.keys())   # Prints all the keys
print (tinydict.values()) # Prints all the values
```
Produces
```console
This is one
This is two
{'dept': 'sales', 'code': 6734, 'name': 'john'}
['dept', 'code', 'name']
['sales', 6734, 'john']
```

Dictionaries have no concept of order among elements. It is incorrect to say that the elements are "out of order"; they are simply unordered. Dictionary *keys*, the first value of each pair must be unique within a dicitonary. Dictionaries are very fast.  

### Adding To A Dictionary

```python
dict = {1:'a',2:'s',3:'d'}
dict[4:'p'] # adds a new key of 4 with a value of 'p'

# to add multiple key/value pairs/
new_dict = {5:'e',6:'g',7:'x'}
dict.update(new_dict)
```



