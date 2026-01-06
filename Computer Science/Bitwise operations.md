---
tags:
  - low_level
---
Bitwise operations are operations that operate directly on the bits of a binary string.
On some [[Processor]]s, bitwise operations can actually be faster than conventional operations like division and multiplication.
This is because bitwise operations are very often directly supported by the [[Processor]], without any kind of abstraction.
# Operations
## NOT
Negation between two bits; inverts the binary.
```
NOT 10101011  (decimal 171)
  = 01010100  (decimal 84)
```
## AND
If and only if both bits are 1, then the resulting bit is 1. Every other case results in 0.
```
    0011 (decimal 3)
AND 0010 (decimal 2)
  = 0010 (decimal 2)
```
## OR
If either of the bits (or both) is 1, then the result is 1. Otherwise, 0.
```
   0101 (decimal 5)
OR 0011 (decimal 3)
 = 0111 (decimal 7)
```
## XOR
Like the OR operation, except that if both bits are 1, the result is 0. So you need to have only one bit at 1 to have a result of 1.
```
    0101 (decimal 5)
XOR 0011 (decimal 3)
  = 0110 (decimal 6)
```
# Bit shifts
The action of pushing a binary value through a [[Register]]. You can push the bits left or right.
There are multiple types of bit shifting, changing the way at which new bits are introduced in the empty spaces created by the movement.
## Arithmetic shift
In arithmetic bit shifts, the bits pushed over the edge of a register are simply discarded. A new 0 is inserted in place of the blank created by the movement, except in a right shift where the leftmost bit is preserved to keep the sign of the number.
```
   00010111 (decimal +23) LEFT-SHIFT
=  00101110 (decimal +46)
```
Preserving the sign:
```
   10010111 (decimal −105) RIGHT-SHIFT
=  11001011 (decimal −53)
```
## Logical shift
Pretty much the same as the arithmetic shift, where 0 is put in place of shifted bits. Any bit pushed out of a register is discarded, including in right-shifts.
## Circular shift

> [!NOTE] Research to be done
> I got lazy when I saw there were two kinds of circular shift, it's up to you, future me!

# Resources
[Wikipedia Article](https://en.wikipedia.org/wiki/Bitwise_operation)
