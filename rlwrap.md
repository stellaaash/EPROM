A tool that is essentially a wrapper on [[GNU readline]].
# Examples
## Better netcat shell
```sh
# Wraps the nc command into rlwrap so you can get a better shell when connecting to 443
rlwrap nc -lvnp 443
```