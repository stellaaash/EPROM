---
tags:
  - algorithm
---
The Dijkstra algorithm allows us to **find the best way from one vertex to all others in  a weighted [[Graph]]**.
# Steps
The basic idea is to store all possible vertices as destinations and their associated weight.
If you find a weight total to go to a vertex that is lower than the previously found weight (from a different path), replace it with the new weight and save the last node before the destination for this path.
This last part effectiveley saves the entire path (since all destinations will have a "best way" saved in the same way).
1. Visit the start vertex
2. Check the weight from the current vertex to all adjacent vertices
3. If the weight of an adjacent edge is lower than the lowest edge so far, save it somewhere along with the vertex connected to it
4. Once step 3 has been done for all edges, visit the lowest-weighted vertex
5. Repeat steps 2 through 4 until we've visited every vertex