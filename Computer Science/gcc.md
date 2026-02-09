---
tags:
  - compiler
---
The GNU Compiler Collection, the Linux specific C compiler. It's pretty good, just like [[clang]], but has more restrictive licenses such that you can't implement it into a project without making it open source. Also, [[clang]] is simply more suited for modern projects that don't require direct Linux kernel interop.

# Options
- `-std=<standard>` : Sets the standard for the code to be compiled. By default, for C, this is `gnu18`. For C++, this is `gnu++17`.
- `-o <name>` : Specify the name of the output executable.
- `-I<directory>` : Specify directory(ies) in which to look for the `#include`d files. 
## Warnings
- `-Wall` : Prints all warnings for things that could be easily fixed or prevented.
- `-Wextra` : Prints even more warnings that aren't printed with `-Wall`.
- `-Werror` : Treat all warnings as errors.
- `-Weffc++` : Some warnings for C++ in case your code violates principles found inside the Effective C++ series of books.
- `-Wconversion` : Warn for conversions that may alter a value.
- `-Wsign-conversion` : Warn for conversions that may change the sign of an integer value.
- `-Wpedantic` / `-pedantic` : Print warnings for every usage of extensions and features that aren't a part of the C or C++ ISO standards.
- `-pedantic-errors` : Treat all usages of extensions and features not part of ISO C and C++ as errors.
## Optimizations
- `-O0` : Disables optimizations. Useful for debug builds.
- `-O2` : Optimizations useful to almost all programs. Useful for release builds.
- `-O3` : More optimizations, sometimes better or worse than `-O2`. Test to see which works best of the two.