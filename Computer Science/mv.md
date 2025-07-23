---
tags:
  - command
  - Linux
---
Move (rename) files.
# Usage
`mv <source file> <new path>`
This "new path" can either be the same name at a different location in the file system, or just a new name to rename the file and keep it in the [[Current Working Directory]].
You can also combine both to rename something AND move it to a different location.
# Option
- `-f` / `--force` : Doesn't prompt when overwriting a file at the destination.
- `-i` / `--interactive` : Prompt when overwriting a file at the destination.
- `-v` / `--verbose` : Print information on what's happening.

# Resources
`man mv`