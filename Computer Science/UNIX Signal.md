---
tags:
---
Signals are ways for **processes to communicate between each other**.
Most of the available signals can be caught by processes, which allows them to behave differently based on specific signals.
The action a process does when receiving a signal is called a *disposition*.
You use the `signal(2)` and `sigaction(2)` functions to **change the disposition of a signal**.
You can set the disposition to either doing the default action, ignoring the signal entirely, or assigning a *signal handler*.
# Default Actions
Signals have a **default action** depending on their meanings, also called a *default disposition*:
- `SIGTERM`: Kills the process but allows it to clean up beforehand
- `SIGIGN`: Ignore the signal.
- `SIGKILL`: Kills the process *immediately*
- `SIGSTOP`: Stops/suspends a process.
- **Core signals**: Their default action is to terminate the process and create a [[Core Dump]].
# Signal Handlers
Signal handlers are **functions that will be executed when a signal is received by a process**.
By default, signal handlers are automatically invoked on the normal [[Process]] [[Stack]].
See `sigaltstack(2)` for how and when to define a new stack for signal handling.

> [!NOTE] Research to be done!
> Was reading section "Synchronously accepting a signal" of `signal(7)`
