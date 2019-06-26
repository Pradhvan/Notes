# Loop better: a deeper look at iteration in Python

* Python does not have a *for loop*.
* Python has a *for each loop.*

```Python
numbers = [1,2,3,4,5,6,7]
squares = (n*n for n in numbers)
```


#### Iterable: 
* Anything that can be iterated over is called an iterable. 
```Python
for item in some_iterable:
    print(item)
```

#### Sequences: 
* Type of iterable in python, eg: lists, tuples etc 
```python
numbers = [1,2,3,4]
cordinates = (1,2,3)
word = 'Hello world'
```
* Sequences are iterables which can be indexed.
* Starts at 0 and ends with one less than the len(sequencs)
* Have features like len,slicing etc

#### Iterable != Sequnces 

* Many objects are iterables but not sequnces i.e sets,files,generators.
```python
my_set = {1,2,3}
my_dict = {'a':1,'b':2}
squares = (n*n for n in numbers)
```
#### How does loops work ? 

* Looping with indexes should be handeled with a while loop.
* This is only valid for a sequnce.
```Python
numbers = [1,2,3,4,5,7]
i = 0
while i < len(numbers):
    print(numbers[i])
    i = i + 1
```
* Sets cannot be indexed 
* Bad practice would be to convert the given set to a list and iterating over it.
```Python
fruits = {'lemon','apple','orange','watermelon'}
i = 0
while i < len(fruits):
    print(fruits[i])
```

* For loops* are powered by **Iterators**
* Iter()* to a sequnce gives us an iterator
* Iterator are like one directional counters that only move in one way ( *next()* ) and cannot be reseted.
* You cannot loop back iterators

```Python
def funky_for_loop_1(iterable,action):
"""A for loop implementation"""
    for item in iterable:
        action_to_do(item)


def funky_for_loop_2(iterable,action):
"""
A for loop implementation in a while loop using iterator,
this is how for loops works internally.
"""
    iterator = iter(iterable)
    done_looping = False
    while not done_looping:
        try:
            item = next(iterator)
        except StopIteration:
            done_looping = True
        else:
            action_to_do(item)
```

* **Iterator Protocal** powers the all the iteration in python.
* **Iterator Protocal** also powers the tuple unpacking in python. (How ?)
```Python
# Tuple unpacking
x,y,z = coordinates
```
* **Iterator Protocal** also powers the star experssions. 
```Python
a,b,*rest = numbers 
print(numbers)
```

* Most of the *built-in* functions that require some kind of looping(iterations) in python user the **Iterator Protocal**

* Generators are also iterators and also iterables (MIND BLOWN !)
```PYTHON
numbers = [1,2,3]
squares = (n*n for n in numbers)
# Gives the generator oject
print(squares)

# Generators are iterators
next(squares) # Result -> 1
next(squares) # Result -> 2

# Initiliazed again because iterators are only one directional
squares = (n*n for n in numbers)

# Generators are also iterable 0-0
for n in squares:
    print(n)
```

* Iter() of an iterator is always the iterator itself. (Inception !)
* Iterators are their own iterators
* Iterators don't know how much item they contain and also can't be indexed. 
* Are single purposed, can only be used for giving the next element( *next()* ) and are exhausted once the iteration is complete.

```Python
numbers = [1,2,3]
iterator1 = iter(numbers)
iterator2 = iter(iterator1)
print(iterator2) # would give an iterator object
print(iterator1 is iterator2) # Result -> True
len(iterator1) # Result -> error
iterator1[0] # Result -> error
list(iterator1) # Result -> [1,2,3]
# Can't be looped over
list(iterator1) # Result -> []
```

### Python't tounge twister  

***Iteratorables are not necessarly iterators but an iterator is  necessarly an iterable.***

*Example:* Generators are iterators that can be looped over but lists are iterables but not iterator.

### Resons to use Iterator:

* Iterators allow lazy evaluation possible which saves memory.
* Iterators allow for infinitely long iterables.

### Not so common iterators

* Enumerate objects are also iterators.
* Zip obects are also iterators.
* Reversed objects are iterators.
* Files are also iterators.

```Python
letters = ['a','b','c','d']
next(enumerate(letters)) # Result -> (0, 'a')
next(zip(letters,letters)) #  Result -> ('a','a')
next(reversed(letters)) #  Result -> 'b'
next(open('iterator.txt')) #  Result -> 'iterator\n'
```
### Creating your own iterator

* Good ways to make an iterator is to make a generator function, not by creating a iterator class. 
```Python
def square_all(numbers):
    for n in numbers:
        yield n**2
```


#### Thingsg to check out:

* Iterator Protocal in more depth.
* Itertools library
* How does iter function work internally.
* Find a very solid diffrence between iterbale and sequence.
* How generators work in python ?
* Looping with indexes in Python
