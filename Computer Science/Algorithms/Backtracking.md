---
tags:
  - programming_concept
---
Backtracking involves [[Recursion]], but after the recursion is done, **you effectively "go back" a step to go down a different route**.
This allows you to explore all possible combinations of different values or "paths".
# Example code
Here's an example of the concept of [[Recursion]] and backtracking, implemented in the form of the rip problem of an exam at 42 school.
The idea is to remove all unclosed parenthesis in a string by replacing them with spaces. Of course, there are usually multiple solutions to each problem.
```C
#include <stdio.h>

int find_difference(char *str) // Find the difference of open and closed parenthesis
{
        int open = 0;
        int closed = 0;
        int difference;

        while (*str)
        {
                if (*str == '(')
                        open++;
                else if (*str == ')')
                        closed++;
                str++;
        }
        difference = open - closed;
        if (difference < 0)
                difference = -difference;
        return (difference);
}

/* Recursively solves the problem by printing when a solution is found and looping over the string,
 * removing a parenthesis at a time and backtracking after the recursive call to go back to the starting state.
 */
void solve(char *str, int depth, int max_depth)
{
        int i;
        char parenthesis;

        if (find_difference(str) == 0)
        {
                puts(str);
                return ;
        }
        i = 0;
        while (str[i])
        {
                parenthesis = str[i];
                str[i] = ' ';
                if (depth < max_depth)
                        solve(str, depth + 1, max_depth);
                str[i] = parenthesis;
                i++;
        }
}

int main(int argc, char **argv)
{
        if (argc != 2)
                return (1);
        printf("[!] - Start with %s\n", argv[1]);
        printf("[!] - Difference is %d\n", find_difference(argv[1]));
        solve(argv[1], 0, find_difference(argv[1]));
}
```
# Resources
[Some cool pdf I found on Illinois education](https://jeffe.cs.illinois.edu/teaching/algorithms/book/02-backtracking.pdf)