---
tags:
---
PSK or Pre-Shared Key is a protocol by which two devices communicate by encrypted messages.
These messages are encrypted using an encryption key that is **the same for both server and client**, thus the name.
You **pre-share the key** by simply placing them in the client and the server, and then setting them up to use it.
They can now communicate pretty securely (see below) via encrypted messages.
# Security
It's good enough for non-critical systems such as monitoring software and other uses, but if you know your system might be the direct target for attacks, you might consider stronger alternatives such as [[Transport Layer Security]] certificates.
In particular, **PSK keys are vulnerable to brute-force attacks**.
This can be heavily mitigated or completely fixed by **using a key that is long enough** that a brute-force attack would take literal years.
# Resources
[Wikipedia](https://en.wikipedia.org/wiki/Pre-shared_key)