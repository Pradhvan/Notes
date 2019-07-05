# Recursion

* The printing(work) part can be done before or after the recursion call.
```Python
def print_1_to_n(n):
    if n == 0:
        return
    print_1_to_n(n - 1)
    # Work done after the recusrion call
    print(n)
    return


def print_n_to_1(n):
    if n == 0:
        return
    # Work done before the call
    print(n)
    print_n_to_1(n - 1)
    return
```
* Work before or after the recusion call is totally diffrent as work after the call will only be excuted when the base case is met and the work done before the recursion call will be done after call.
* Thus the above two function give very diffrent with a slight change of print statement.
* There can be more than two base cases for recursion
```Python
def fib(n):
    if n == 1 or n == 2:
        return 1
    fib_n_1 = fib(n - 1)
    fib_n_2 = fib(n - 2)
    output = fib_n_1 + fib_n_2
    return output
```
* Python by default has a recursion limit and even if you're code is correct but has to perform large computations, you can change that limit from *sys*.
```Python
import sys
n = # Very large number here
sys.setrecursionlimit(n)
```
