---
tags:
  - algorithm
  - sorting
---
A simple **sorting algorithm** whose concept is just stepping through the list element by element, comparing the current element with the next one, and **swapping** the two if needed.
Bubble sort has an efficiency of **O(n^2)**
# How it works
You do multiple passes (since it's impossible to sort everything by just swapping in one pass) until all values are sorted.
You know that you have a sorted array when you do a pass that doesn't need any swapping.
# Optimization
You can optimize it a little by knowing that **at each pass, the value you bubbled all the way up is now in the correct position**, so you can lower the max index to loop at by one.