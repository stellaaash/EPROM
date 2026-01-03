---
tags:
  - data_structure
---
Binary Heaps are [[Heap]]s that are also a kind of [[Binary Tree|Binary Tree]] with these two main conditions:
- Its heap condition is that the value of each node must be greater than each of its descendant nodes.
- The tree must be complete, which means that **all nodes must be present on all tree levels, except for the last level which can have missing nodes towards the right**.
# Underlying Implementation
While the obvious implementation would use linked nodes, there is actually a better way, especially for Binary Heaps: *arrays*.
Yup. Actually, you can put every node in a binary heap in an array, ordering them in the latter by tree levels from left to right.
Essentially, you just put all the levels in order in the array, from left to right.
Thanks to this, **the Last Node is always gonna be the last array element**, fixing the problem of actually finding that node without iterating over the entire heap.