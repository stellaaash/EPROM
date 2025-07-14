---
tags:
  - C
  - cheatsheet
---
A C software library that provides in-line edition and history capabilities for interactive programs with a command-line interface for example, like [[Bash]]. Part of the [[GNU Project]].

> [!WARNING] `readline` vs `libedit`
> One needs to be careful coding using `readline` related functions on [[macOS]], because it has (same as pretty much all the [[libc]]) a different implementation than GNU readline, specific to [[BSD]] systems, called `libedit`.

# Key bindings
A lot of key bindings are directly taken from the [[Emacs]] text editor.
The `ctrl` key is stylized as a `^`.
- `^a` : Moves caret to start of line
- `^c` : Sends [[SIGINT]] to the current running process.
- `^d` : Sends an EOF character which makes the `readline()` function return NULL. In [[bash]], for example, closes the shell.
  Also technically removes the next character if not at the end of the line.
- `^e` : Moves caret to end of line.
- `^l` : Clears the screen contents (equivalent to [[clear]]).
- `^n` : Moves down the history, towards the more recent commands. Like pressing `↓`.
- `^p` : Moves up the history, towards the older commands. Like pressing `↓`.
- `^t` : Transposes (or swaps) the two previous characters.
- `^u` : Cuts the contents before the caret.
- `^v` : Allows to write literal [[Control Sequence]]s to the line (pressing `^v^h` writes literally "^H" to the prompt, an actual backspace character).
- `^w` : Cuts the word before the caret.
- `^y` : Yank, or paste from the clipboard at caret.
- `Alt+b` : Brings back the caret by one word.
- `Alt+f` : Advances the caret by one word.
# Resources
`man 3 readline` on a [[Linux]] that has the `readline` library installed.
[Wikipedia Article](https://en.wikipedia.org/wiki/GNU_Readline)