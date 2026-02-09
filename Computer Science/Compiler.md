---
tags:
---
A program which reads compiled languages source files and translates them into another programming language (often directly machine code to be executed).
Usually starts by preprocessing, followed by compilation and then linking of [[Object File]]s.
Some compilers can also be configured to translate source code into [[Assembly]] for study (which would then be run through an [[Assembler]] to be turned into machine code).

> [!ERROR] Portability
> The resulting executable programs coming from a compiler are very rarely portable from platform to platform!
> Since they are written directly in machine code targeting the architecture it was compiled on, it cannot easily switch computers and still function!
> For example, compiling a program under [[macOS]] would result in an executable impossible to run natively on [[Windows Registry]], for example.
> This is because **each [[Operating System]] has its own executable format:** [[Executable and Linkable Format]] for Linux/Unix, [[Portable Executable]] for [[Windows Registry]], [[Mach-O]] for [[macOS]].

Importantly, compilers are also responsible for syntax checking and error checking, raising appropriate warnings and errors when your code doesn't meet the mark, and aborting the compilation process if needed.
The object files created by the compiler are then linked by the linker into an executable. It will also link it with any libraries that are used, often including the standard library of the source language.
# Examples of Compilers
- [[GCC]]
- [[clang]]
- The Rust Compiler
- ...