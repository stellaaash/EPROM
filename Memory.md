---
tags:
  - programming_concept
---
Memory, or Random Access Memory (RAM) is the main storage of memory for an operating system at runtime.
# 64-bit [[Linux]] Process Memory Map
In a 64-bit Linux environment, a process memory map typically includes:

- **Text Segment:** Contains executable code.
- **Initialized Data Segment:** Stores global and static variables initialized by the programmer.
- **Uninitialized Data Segment (BSS):** Holds uninitialized global and static variables.
- **Heap:** Dynamically allocated memory managed by `malloc()`, `realloc()`, and `free()`.
- **Stack:** Memory for function call frames, including local variables and return addresses.
- **Memory-mapped Regions:** Used for shared libraries and files mapped into memory.

A simplified map looks like:

```
|-----------------------------|
| Stack (grows downward)      |
|-----------------------------|
| Memory-mapped segments      |
|-----------------------------|
| Heap (grows upward)         |
|-----------------------------|
| Uninitialized Data (BSS)    |
|-----------------------------|
| Initialized Data            |
|-----------------------------|
| Text Segment (code)         |
|-----------------------------|
```
# Stack vs Heap
- **Stack Memory:** Automatically allocated and deallocated for local variables and function calls.
- **Heap Memory:** Dynamically allocated using functions like `malloc()` and `free()` (for [[C]]).
# Virtual vs Physical Memory
Physical memory refers to the entire memory attached to the system, usually in the form or RAM sticks.
Virtual memory, on the other hand, refers to the part of that physical memory that is allocated for a singular process.
This gives the process the illusion it has access to the entire memory space, and allows it to freely use that virtual space as it pleases.
There's a translation layer between the virtual memory addresses and the physical, actual adresses on the RAM.
This translation barely has an impact on the read/write performance on RAM from the process' point of view, but it's important to know it's there.
# Checking the memory maps of a process
`cat /proc/self/maps` prints out the list of maps used by the cat process you just created.
# Resources
[Wikipedia - Virtual Memory](https://en.wikipedia.org/wiki/Virtual_memory)