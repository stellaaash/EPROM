---
tags:
  - algorithm
---
In a sorted [[Array]], Binary Search allows for **efficient looking up of values** by repeatedly slicing the array in half until the value is found.

For example, when looking up a number in a sorted array of 100 numbers, you'd first check the one at the middle.
Then, if the number found is lower, leave the entire left half of the array to the side (since the number has to be on the right because it is higher) and split the new slice in half.
Vice-versa if the number found is higher.
Rinse and repeat until the number is found (or it can be certified the number isn't part of the sorted array).