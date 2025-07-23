In [[bash]] and other [[Unix]] shells, heredocs are a type of redirections of sorts. You use them like `less << EOF`, where [[less]] is the command, and `<< EOF` is the heredoc itself.
More generally, a here document is a part of a file that is treated as a completely different file. That's why it works the way it does in [[bash]], replacing input from actual input files with the input of a particular part of the terminal.
# How it works
What it does is effectively replace the input [[File Descriptor]] from less with the input from the heredoc. One way to implement this is calling [[GNU readline()]] until the delimiter is found as a complete line, then ending the heredoc and sending the entire input to the command.
```bash
# > cat << EOF
> wow
> wow
> EOF
wow
wow
```
# Resources
[Wikipedia article](https://en.wikipedia.org/wiki/Here_document)