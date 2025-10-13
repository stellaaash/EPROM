---
tags:
  - C
  - cpp
---
Clang is part of the [[LLVM]] project and as such, directly integrates it into its compilation system.
The most notable difference between [[gcc]] and clang is the IR, or Intermediate Representation ; this allows [[LLVM]] to perform heavy optimizations on the code being compiled. The process is basically like this :
[[Compiler]] (clang, zig, ...) generates IR code -> [[LLVM]] takes in the IR and optimizes it -> the appropriate back-end (in the case of clang, C) generates optimized machine code from the IR`
Another notable difference is that clang is more user friendly and can easily cross-compile to multiple targets. Its [[LLVM]] back-end ensures that many platforms can be used as targets.
# Common options
## Sanitizers
With the `fsanitize=<>` flag, you can provide runtime checks that are to be added at compilation. Here are some of the most useful ones:
- `address`: Checks for buffer overflows, use-after-frees and memory leaks to a lesser extent
- `leak`: Checks for memory leaks
- `memory`: Checks for uninitialized reads
- `undefined`: Checks for undefined behavior (particularly useful here as unavailable in [[Valgrind]])

Most are mutually exclusive, which means you can't use them at the same time. However, a good combination is `-fsanitize=address,undefined,leak`.