---
tags:
  - data_structure
---
A number of elements in a specific order.
Depending on the programming language, all elements must be of the same type.
# Accessing the data
Accessing elements in an array is usually done by providing an index number `n`, and the array will look at the `n`-th element stored inside.
Most arrays start at element `0`, with the notable exception of Lua and some other languages starting at `1` instead.
# Time Complexity
## Reading
Since array indexes are memory addresses, accessing one takes **O(1)** time.
## Searching
Searching through an array involves sequentially reading all elements.
As such, searching takes **O(n)** time, where n is the length of the array.
Worst case scenario is when the array does not contain the searched item, and the search must then iterate over the entire array, thus providing the O(n) speed.
## Insertion
Insertion is easy if you're adding an item at the end of the array, but it gets dicy if you insert it in the middle or at the beginning.
In such cases, items coming afterwards the new item have to be shifted.
As such, inserting's worse case is **O(n+1)**, where N is the number of elements in the array.
## Deletion
Just as for insertion, deleting an array element means shifting all further elements back into the empty spot created.
As such, deletion's worse case is **O(n)**, where n is the number of elements in the array.
# Resources
[Wikipedia](https://en.wikipedia.org/wiki/Array_(data_structure))