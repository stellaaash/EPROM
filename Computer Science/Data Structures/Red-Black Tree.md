---
tags:
  - data_structure
---
A red-black tree is a **self-balancing [[Binary Search Tree]] where each node contains an extra bit determining the color of the node** (either red or black).
![](https://cdn.programiz.com/sites/tutorial2program/files/red-black-tree_0.png)
# Key rules
1. Each node is **either red or black**.
2. The root node is **always black**.
3. **No** two red nodes **can be adjacent** (a red node cannot have a red child, for example).
4. Every path from any node to its descendant leaves (NULL nodes) contains the same number of black nodes.
5. All leaves are considered black.
