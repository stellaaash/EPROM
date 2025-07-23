---
tags:
---
Unicode is a **standard for representing and managing text in most of the world's writing systems**.
Almost all modern software that works with text, works with that text in Unicode.
Every year, a new version of that standard gets published (including new emojis, for example).
# How it works
## Code points vs Code units
These concepts are very important to understand how Unicode works under the hood:
- Code points are **numbers that represent the atomic parts of Unicode text**.
  Most of them represent visible symbols, but they can also have different meanings, like specifying an aspect of the symbol.
  This can include changing the accent of a letter, the skin tone of an emoji, etc...
- Code units are **numbers the encode code points**, to store or transmit Unicode text.
  One or more code units encode a single code point.
  **Each code unit has the same size**, which depends on the encoding format being used.
  The most popular format, UTF-8, has **8-bit code units**.
## Encoding Unicode code points
The size of a code point nowadays (2025) is **21 bits**. These 21 bits are partitioned in 17 planes, with 16 bits in total.
The main ways to encode code points is called **Unicode Transformation Format (UTF)**, and there is three versions of that technique:
- **UTF-32: 32 bits**
  Has one code unit per code points. This is the only one with **fixed-length encoding**.|
  All others use a varying number of code units to encode a single code point.
- **UTF-16: 16 bits**
  In UTF-16, the BMP (first 16 bits of Unicode) is stored in single code units.
  <...>
- **UTF-8: 8 bits**
  Since UTF-8 uses 8-bit code units, it always uses 1 to 4 code units to encode a single code point.
  

> [!TODO] Research to be done!
> I got lazy on the specifics of how the binary works in UTF-16 and 8, look it up when you want to!
## Grapheme clusters
Since a lot of languages think of singular "characters" very differently, Unicode also has different ways of thinking about a singular "character".
Graphemes are one of these. It corresponds as closely as possible to a symbol displayed on screen or paper.
It is also sometimes called a "user-perceived character", notably in the official Unicode documents.
## Glyphs
Glyphs are what is being used when actually drawing characters on screen.
For example, when writing the letter `à`, the OS might use the `a` glyph combined with the \` glyph.
