## Python's Infamous GIL : Larry Hastings

```PYTHON
a = []
b = a
'''Current ref count it three as we 
  created a new ref when passed it 
  through the getrefcount()
'''
sys.getrefcount(a) #3
```
* Multiple locks can lead to deadlocks,i.e: One lock per global variabale, one lock per group of global,refrence count locks




### Things to check out:
* Race conditions 
* 
