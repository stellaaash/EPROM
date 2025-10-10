---
tags:
  - data_structure
---
A collection of **unique** elements.

# Implementations of sets
There are multiple ways to implement a set, some are more straightforward than others.
Some of the special ones include:
- [[Hash Set]]
- [[Tree Set]] - Maintains the order
- And more...
# Time Complexity
(for [[Array]]-based sets)
Since these sets don't allow for duplicates, their complexities are slightly different, especially for adding values.
## Reading
Same as for arrays, **O(1)** as it is jumping to an address in memory.
## Insertion
Since insertion involes checking the entire array for the inserted value (no dupes can exist), the best case would be **(n+1)** and the worst case is **O(2n+1)**.
N is the length of the set.
## Search
**O(n)**
## Deletion
**O(n)**