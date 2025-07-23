---
tags:
  - programming_concept
  - C
---
Mutex, short for "mutual exclusion", is **a kind of "lock" on data that you want to "protect" between [[Thread]]s**.
Used well, they effectively prevents race conditions : when a thread wants to update a static variable (shared between threads), it locks the associated mutex (that YOU will have set in the code) to tell all other threads to wait if they arrive to that part of the code.
# How it works
Each thread can *acquire* or *release* a mutex (you also say *lock* and *unlock*). When one thread acquires it, any other thread that tries to do so must wait for the first one to release (or unlock) it. In the meantime, it can continue execution freely (and eventually release the mutex).
While "waiting" for the mutex to unlock, a thread is put to sleep. If multiple threads are waiting on a mutex when it unlocks, a seemingly random thread gets access to it and locks it. Rinse and repeat.
In theory, **you should keep a mutex locked for as short of a time as you can**. Do one mutex per variable or struct, do your changes, then unlock it immediately so it doesn't hinder the other threads too much.
## In C
Initialize a mutex with `mtx_init()`, then lock and unlock with it `mtx_lock()` and `mtx_unlock()` respectively.
Once a mutex isn't needed anymore, destroy it with `mtx_destroy()`.
### Code example
> Code example blatantly stolen from Beej's guide to C programming
```C
#include <stdio.h>
#include <threads.h>

mtx_t serial_mtx;    // <-- MUTEX VARIABLE

int run(void *arg)
{
	(void)arg;
	
	static int serial = 0; // Shared static variable!
	
	// Acquire the mutex--all threads will block on this call until
	// they get the lock:
	
	mtx_lock(&serial_mtx);
	
	//<-- ACQUIRE MUTEX
	
	printf("Thread running! %d\n", serial);
	
	serial++;
	
	// Done getting and setting the data, so free the lock. This will
	// unblock threads on the mtx_lock() call:
	
	mtx_unlock(&serial_mtx); // <-- RELEASE MUTEX
	
	return 0;
}

#define THREAD_COUNT 10

int main(void)
{
	thrd_t t[THREAD_COUNT];
	
	// Initialize the mutex variable, indicating this is a normal
	// no-trills, mutex:
	
	mtx_init(&serial_mtx, mtx_plain); // <-- CREATE MUTEX
	
	for (int i = 0; i < THREAD_COUNT; i++) {
		thrd_create(t + i, run, NULL);
	}
	
	for (int i = 0; i < THREAD_COUNT; i++) {
		thrd_join(t[i], NULL);
	}
	
	// Done with the mutex, destroy it:
	
	mtx_destroy(&serial_mtx); //<-- DESTROY MUTEX
}
```
# Mutex types
Some of these mutex types are the result of [[Bitwise operations]].

| Type                       | Description                            |
| -------------------------- | -------------------------------------- |
| `mtx_plain`                | Regular mutex                          |
| `mtx_timed`                | Mutex that supports timeouts           |
| `mtx_plain\|mtx_recursive` | Recursive mutex                        |
| `mtx_timed\|mtx_recursive` | Recursive mutex that supports timeouts |
*Recursive* means that the holder of a lock can call `mtx_lock()` multiple times on it. Useful when you've got nested permissions that could require multiple levels of locking, or you just have a function that needs to lock it multiple times.
Just be careful to also unlock it the same amount of times.
# Resources
Chapter 39.7 of Beej's guide to C programming
[Wikipedia Article](https://en.wikipedia.org/wiki/Lock_(computer_science))
