# Async Techniques and Examples in Python

#### Threads

* Threads don't really let us levrage the multile cores to do actual concurrent CPU bound opertion in Python
* Most libraries aren't built for Asyncio in those time threads come into picture for corcurrency.

```PYTHON
import time 
import threading 

def main():
    t = threading.Thread(target=greeter, args=('Pradhvan', 100))
    t.start()
    print("I am done !!!")

def greeter(name, times):
    for i in range(0, times):
        print("Hello there {}".format(name))
        time.sleep(1)


if __name__ == '__main__':
    main()
```
* Threads in python are foreground threads.
