---
tags:
  - algorithm
---
Quicksort is a part of [[Sorting Algorithms]], and involves recursively dividing an array into partitions and sorting these around pivots.
# How it works
The algorithm functions in a recursion of partitions.
1. You partition an array (described below). The pivot is now in the right spot in the array.
2. Partition again on the two subarrays around the pivot
3. Rinse and repeat until you end up with a subarray of 1 or 0 element.
## Partitionning
Partitionning involves selecting an arbitrary **pivot value** in the array. Often, this is the rightmost value of the current partition (or subarray, when you recurse).
You then **set two pointers to the rightmost and leftmost values** in the subarray.
You walk them element by element towards the center of the array until both:
- The left pointer points to an element higher than the pivot
- The right pointer points to an element lower than the pivot
If that's the case, **swap the two pointers' values** and keep going.
Otherwise, you **swap the left pointer's value with the pivot's** and start recursion on the two surrounding subarrays.