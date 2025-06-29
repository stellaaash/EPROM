---
tags:
  - file_format
---
Also called **ELF**, the Executable and Linkable Format is a standard often used for compiled executables, [[Object File]]s, libraries and [[Core Dump]]s.
It was first created for the Unix family of systems.
# Composition
Each ELF file contains an ELF header, followed by the actual file data.
There are generally several key segments inside an ELF:
## Segments
- `.text`: The executable code of the program. Usually marked as read-only and executable.
- `.data`: Global and static variables. This segment is writable.
- `.bss`: Uninitialized global and static variables. Allocated in memory at runtime to be modified by the program.
- `.rodata`: Read-only data, like string literals and constant variables.
- `.dynamic`: Used for dynamic linking, has information used by the linker to load shared libraries and resolve symbols at runtime.
- `.got`
- `.plt`
- `.init`: Initialization code to be executed before the `main()` function.
- `.fini`: Cleanup code to be executed after the `main()` returns.
- `.comment`: Version control information or other metadata.
- `.note`: Various notes, such as build information or other metadata.
- `.symtab`: Symbol table with information about symbols (variables, functions) used in the program.
- `.strtab`: String table for the names of the symbols in `.symtab`.
# Resources
[Wikipedia](https://en.wikipedia.org/wiki/Executable_and_Linkable_Format)