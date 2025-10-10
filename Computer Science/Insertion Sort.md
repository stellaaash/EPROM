---
tags:
  - algorithm
---
Insertion sort works by **inserting wrongly-placed elements of an array in their right place** in multiple iterations.
Detailed, the process looks like this:
1. Iterate over the array until an out-of-place value is found
2. Grab it (put it in a temp variable)
3. Shift all previous elements forward until the right spot for the temp variable is found
4. Insert the temp variable in the newfound empty spot behind the two variables above and below it
5. Start a new pass from the slot of the newly placed value