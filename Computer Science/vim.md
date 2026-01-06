---
tags:
---
**The** perfect text editor.
An in-terminal text editor to edit text files, code and do a lot of stuff.
Its commands are so ergonomic and fast to use they have been exported and reused in a variety of other software.
Most modern IDEs have plugins or builtin support for vim motions.
# Derivatives
[[nvim]]
[[vimium]]
# Vim modes
## Normal mode
In this mode, Vim motions and actions can be used. You can easily move around the document and make light edits with commands such as `r` and `x`, or enter another mode, copy and paste, delete entire lines, etc...
## Insert mode
In this mode, you are directly editing the document like you would be if you opened it in [[nano]] or another standard text editor.
## Visual mode
In this mode, you are selecting parts of the document to be modified, copied etc...
You can move around using vim motions and do actions just like you would in normal mode, but your actions are performed on the selected text instead of a single character.
## Ex mode
Used to input commands using the `:` shortcut.
# Cheat sheet
The cheet sheet motions, commands and actions found below are to be executed in normal mode.
## Vim motions
- `hjkl` : **Move one character** left, down, up and right respectively.
- `w`: Go to the **beginning of the word**.
- `e` : Go to the **end of the word**.
- `b` : Go to the **beginning of the last word**.
- `0` : Go to the **beginning of the line**.
- `$` : Go to the **end of the line**.
- `^b` : **Go Back** - Scroll up one page.
- `^f` : **Go Forward** - Scroll down one page.
- `^d` : Scroll **Down half a page**.
- `^u` : Scroll **Up half a page**.
- `'.` : Jump to **last modification line**.
## Vim actions
- `i` : Enter **insert mode** before the caret.
- `a` : **Append** : Enter insert mode after the caret.
- `A` : **Append after line** : Enter insert mode at the end of the line.
- `o` : Create **new line after caret** and enter insert mode there.
- `O` : Create **new line before caret** and enter insert mode there.
- `v` : Enter **visual mode** (selection mode).
- `V` : Enter **visual line mode** (visual mode with all whole line selected).
- `y` : **Yank**, or **copy** selection into the clipboard.
- `yy` : **Yank** the current line.
- `x` : **Cut** the selection into the clipboard.
- `p` : **Puts** or **paste after** the caret.
- `P` : **Puts before** the caret.
- `d<motion>` : **Delete** the text covered by the motion.
- `dd` : **Delete** the **entire line**.
- `D` : **Delete** from the caret to **the end of the line**.
- `c<motion>` : **Change** the text covered by the motion : delete and enter insert mode.
- `cc` : **Change** the **entire line**.
- `C` : **Change** from the caret to **the end of the line**.
- `u` : **Undo** last change.
- `^r` : **Redo** next change.
- `/<query>` : **Search** query from cursor onwards.
- `?<query>` : **Search** query before cursor.
- `.`: **Repeat** last action.
## Vim commands
- `:h` : Shows the **help menu**.
- `:w` : **Write**, or **save** the current file.
- `:q` : **Close** the current file. Closes vim if this is the only file currently opened.
- `:q!` : **Force close**. Will close without prompting to save files.
# Resources
[LearnXinYminutes.com](https://learnxinyminutes.com/vim/)
