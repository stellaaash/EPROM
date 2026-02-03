
# 64-bit [[Linux]] Process Memory Map
In a 64-bit Linux environment, a process memory map typically includes:

- **Text Segment:** Contains executable code.
- **Initialized Data Segment:** Stores global and static variables initialized by the programmer.
- **Uninitialized Data Segment (BSS):** Holds uninitialized global and static variables.
- **[[Heap]]:** Dynamically allocated memory managed by `malloc()`, `realloc()`, and `free()`.
- **[[Stack]]:** Memory for function call frames, including local variables and return addresses.
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
- **Heap Memory:** Dynamically allocated using functions like `malloc()` and `free()` (for C).