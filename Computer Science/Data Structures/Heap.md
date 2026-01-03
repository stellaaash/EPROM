---
tags:
  - data_structure
---
Heaps are kinds of [[Tree]]s.

# Operations
## Insertion
Inserting a new node in a heap goes a little bit like this:
1. Put the new node as the last node initially
2. Compare it to its parent node, if the heap condition isn't satisfied, swap the two's values
3. Rinse and repeat until the heap condition is satisfied
## Deletion
1. Delete the top node
2. Put the Last Node as the top node
3. Check both children to see which one is larger (or smaller in cases of min-heaps, the important is **choosing the node that wouldn't violate the heap condition if swapped with the trickle node**)
4. If the trickled node is smaller than this one, swap the two values
5. Repeat step 3 and 4 until the heap conditoon is satisfied (and the trickle node has no children greater than it)
# Heap Condition
Heap conditions are requirements that a heap fulfills in regards to how the elements are sorted vertically (through its levels).
For example, a *max-heap* makes it so that every element only has descendants lower than itself.
A *min-heap*, on the other hand, does the exact opposite.
Both of these are often implemented as a [[Binary Heap]].
# Last Node
The last node in a heap is **the rightmost node of the bottom level**.
# Trickling
Trickling is the process of swapping values to move a node until the heap condition is satisfied.
Used in both insertion and deletion operations.
When trickling a node, it is called the *trickle node*.