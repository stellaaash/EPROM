---
tags:
port: "22"
---
Secure Shell protocol or SSH allows for **secure, remote communications between two hosts**.
It is essentially the secure version of [[telnet]], though better in almost every way.
# Security
SSH uses [[Public-key Cryptography]] to secure connections, with public and private keys.
**`ssh-keygen` is a handy program to create such keys.**
SSH private keys can be given a passphrase to add an additional layer of encryption over them: to use the private key, you must first provide the passphrase.
The `.ssh/authorized-keys` lists allowed keys that can be used to connected to the local server. Adding a key inside of it can be a useful backdoor when penetration testing.