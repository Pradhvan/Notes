# Understanding the Python GIL: David Beasly


### Python Threads
* Python uses *real* system thread (POSIX Threads ? )
* Managed by the host operating system 
* Parallel execution is forbidden by *GIL*
* When a thread is running it aquiers a GIL 
* GIL is released on I/O (read, write, send , recieve) --> *I/O bound processed*
* *CPU Bound* threads that never perform I/O (computation tasks ??) are treated in special case, a check occurs every 100'th *ticks* 
* Tick is loosely one machine instruction
* *Check* reset's the counter to 100 (That's why 100 ticks) --> Relases the GIL -->Reacquires the GIL 
* The above is also called thread switching in Python 
* GIL is an instance of a lock 
* Thread switching in I/O bound processes: When one thread is running and after some time realeases the GIL due to some I/O bound task.
#####  *---Python2 Case---*

*   It usualy sends a singnal to the *Pthread* libarary and gets the OS to switch to the other thread i.e the other thread acuires the GIL and runs. 
* What happens when a process runs into a check and it is forced to give up the GIL so that other process and run ?


*First Case:* It might release the GIL but the OS might give it back due to it's high prioriry 
*Second Case:* It might release the GIL and the OS might assign it to the other thread beacuse it's of higher priority. 

* The Pthreads library has the waiting queue in which every thread is deposited when it asks for the GIL and is released on the signal operation.
* Once the thread is poped off by a signaling operation it joins the ready queue of the OS where it competes with other processes and the thread with the highest priority wins.

##### *---Python3 Case---*

GIL in Python3 when one thread is running and other is suspended.

*First Case:*  Suspended thread waits for the for the active thread to do an I/O bound task and than acquires the GIL when the active thread releases the thread. 

*Second Case:* The suspended thread sends a drop request forcing thread one to stop after what it's doing and release the GIL.

The two threads have a signaling mechanism which tells the previous active thread through an ack that the GIL is recieved and than the previous active thread is suspended. 

### Problems with GIL:
* Increase response time as after the drop request it has to wait a bit which seems like a *poor response time* to the end user. Ignores the high priority of the I/O or events
* Most deserving thread may not recieve the thread and some other thread might recieve the thread and the thread that has to recieve the GIL goes into timeout again.

### THINGS TO CHECK OUT !! 

* What the heck is a lock ? What it has to do with a process ? 
* Mutex lock 
* Conditional Variable in OS 
* Scheduling process in OS 
* system level scope vs the process level scope 
* Byte code and How python produces byte code 

