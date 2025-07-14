---
tags:
  - Unix
  - programming_concept
  - C
  - POSIX
---
**Threading is the concept of splitting the load of a particular [[Process]] across multiple [[Processor]] cores.** You can have more threads than cores on most [[Operating System]]s, it's usually the OS itself that will balance the threads between the cores.
# How it works
In C programming, for example, you create a new thread using the `pthreads` library (POSIX threads) (make sure to link it with your executable using `-lpthreads`~) by specifying the function that that thread will run. Kind of like your program starts at `main`, the thread will start a function YOU specify. Within limits, of course.
You then let the thread run while the parent thread (the `main`) still works in parallel.
You can then wait for the thread to complete, by *joining* it.
A thread can `exit()` or end its own life by returning from the "main" function you gave it.
A thread can also sleep for a period of time, not hindering other threads of a [[Process]].
## Thread memory
Threads have shared heap and data memory sections (also with the main thread), allowing easy but dangerous (see below) communication between different threads. That also means that there's no need to free a heap variable in all threads, like with [[Child Process]]es.
The [[Stack]] is the only one that's not shared.
If you put a `static` variable in the function that a thread will run, all the threads will be able to see and modify the same value, which could easily lead to race conditions.
You can use the `_Thread_local` type to say that a static variable shouldn't be shared between threads.
## Detaching threads
Using `thrd_detach()`, you can tell a thread to keep on executing on its own, without needing to `wait()` for it. But that also means you lose the option to get its return value once it exits.
## Thread safety and race conditions
Since threads share their memory spaces, you can easily end up in something known as a "race condition", or "data race". In a nutshell, this is when two or more threads are trying to access and/or modify the same value at the same time. This can very easily cause said value to become completely corrupted with part of the first thread's modification and part of the second's.
Thing is, **this isn't limited to only conventional variables you might set in your code.** This is pretty much to take into account for any resource that might be shared between threads. Ring any bells? That's right! Enter the standard input and output. What if two threads try to write something to stdout at the same time? You'll end up with two outputs mixed together, resulting in a garbled output. Not something we want. That's why we have concepts such as [[Mutex]]es.

> [!WARNING] The C standard library and race conditions
> Careful with some functions in the standard library that may keep a variable somewhere to keep states! If a standard libc function keeps a state between calls, it's probably not thread safe and needs protection set around that function.

# C Program example
Threads are identified with variables of type `thrd_t`, basically the ID of the thread (though it is an [[Opaque Variable]]).
You **create threads** with `thrd_create()` and join them with `thrd_join()`. Pretty straightforward, except the first one takes in a pointer to the function the new thread is supposed to execute once it starts.
It can also take in arguments to pass to the function that's gonna be run in the form of a `void *`. **Careful, that data has to have a lifetime long enough to be sustained throughout the thread's runtime.**
You store the **return value** of a thread by passing a pointer to `thrd_join()`.
## Code
> Example code taken from Beej's guide to C programming.
```C
#include <stdio.h>
#include <threads.h>

// This is the function the thread will run. It can be called anything.
//
// arg is the argument pointer passed to `thrd_create()`.
//
// The parent thread will get the return value back from `thrd_join()`'
// later.

int run(void *arg)
{
	int *a = arg; // We'll pass in an int* from thrd_create()
	
	printf("THREAD: Running thread with arg %d\n", *a);
	
	return 12; // Value to be picked up by thrd_join() (chose 12 at random)
}

int main(void)
{
	thrd_t t; // t will hold the thread ID
	int arg = 3490;

	printf("Launching a thread\n");

	// Launch a thread to the run() function, passing a pointer to 3490
	// as an argument. Also stored the thread ID in t:
	
	thrd_create(&t, run, &arg);
	
	printf("Doing other things while the thread runs\n");
	
	printf("Waiting for thread to complete...\n");
	
	int res; // Holds return value from the thread exit
	
	// Wait here for the thread to complete; store the return value
	// in res:
	
	thrd_join(t, &res);
	
	printf("Thread exited with return value %d\n", res);
}
```
# Resources
Chapter 39 of Beej's guide to C programming
`man pthreads` on a [[Linux]] system.
