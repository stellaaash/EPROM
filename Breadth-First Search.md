---
tags:
  - algorithm
---
Breadth-First Searching a [[Graph]] or a [[Tree]] involves using a [[Queue]] to iterate over all connected vertices starting at a given vertex.
You keep all visited vertices so that we don't loop infinitely.
# Algorithm
The algorithm is basically starting at the vertex, inserting all the connected vertices in a queue and looping over that queue.
Each time a new vertex is accessed, we add all of its connected vertices to the queue.
**This enables iterating over each layer of connected vertices at a time** instead of recursively iterating over all the layers and then climbing back up.