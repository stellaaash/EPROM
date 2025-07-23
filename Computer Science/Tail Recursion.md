---
tags:
  - programming_concept
---
Tail recursion is a type of recursive function that performs its recursive call as the last part of the function. This allows the [[Compiler]] or [[Interpreter]] to perform optimizations, heavily reducing the [[Stack]] size growth with each recursive call compared to a recursion with no tail recursion.
To be clear, not every recursive [[Algorithm]] will allow you to do tail recursion, but if you can squeeze that in, especially if you know the recursive function is going to go many levels deep, it's probably a good idea to do it.
Of course, it is impossible to do tail recursion when [[Backtracking]].
# Difference in practice
## With no tail recursion
```C
int recursive(int i)
{
	i++;
	if (i < 10)
		recursive(i);
	printf("%d", i);
}
```
## With tail recursion
(listen I know I literally just removed the `printf` call, I just couldn't come up with a better example sorry)
```C
int recursive(int i)
{
	i++;
	if (i < 10)
		recursive(i);
}
```