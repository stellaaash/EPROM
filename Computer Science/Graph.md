---
tags:
  - data_structure
---
A collection of nodes connected by edges, representing relationships between entities.
They're often used to model social networks, computer networks, transportation networks, among other stuff. Mostly networks.
They consist of **vertices** (nodes) and **edges** (connections between nodes).
A graph where all vertices are connected in some way is called a *connected graph*.
# Accessing the data
There are multiple [[Algorithm]]s for accessing the data within a graph, including:
- Breadth-First Search
- Depth-First Search
# Graphs vs Trees
[[Tree]]s are types of graphs, which means that **not all graphs are trees, but all trees are graphs**.
In fact, trees are just graphs that respect a few rules:
1. They must not have *cycles* (nodes that reference each other circularly)
2. All nodes must be connected
# Resources
[Wikipedia](https://en.wikipedia.org/wiki/Graph_(abstract_data_type))