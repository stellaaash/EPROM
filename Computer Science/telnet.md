---
tags:
  - networking
port: "23"
---
Telnet is a client-server application protocol that provides access to virtual terminals or remote systems on local networks or the Internet.
It is a protocol for **bidirectional 8-bit communications**.
Its main historical goal was to connect terminal devices and terminal-oriented processes.
# Cheatsheet
```sh
telnet [options ...] [host [port]]

> <interesting options and examples here>
```
# Security
Telnet transmits all communications, including usernames and passwords, in plain text.
This major vulnerability disqualifies telnet for any communication that might contain sensitive information.
# Uses
Telnet is often used in legacy equipment that doesn't support more modern communication protocols.
It is also sometimes used by [[Amateur Radio]] operators for providing public information.
Most useful of all, though, is its uses when **debugging network services such as [[Simple Mail Transfer Protocol]], [[Internet Relay Chat]] or [[HyperText Transfer Protocol]] servers**.
You can use it to issue commands to the server and examine the responses, examining them or just to see if a [[Service]] is up.
# Resources
[Wikipedia]([Telnet - Wikipedia](https://en.wikipedia.org/wiki/Telnet))