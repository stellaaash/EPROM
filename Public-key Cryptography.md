---
tags:
  - networking
---
Public-key Cryptography is the process of creating a secure communication between two parties using a combination of a public and a private key.
# How it works
When establishing communications, two parties using the public-key cryptography paradigm will do simple but intricate exchange of encrypted information:
- The server creates a private and public key that is going to be used for communications.
- As its name implies, the public key is broadcast to anyone that wants to talk with the server securely.
- Any client that wants to talk to the server can encrypt their packets using the public key.
  **Only the private key the server holds can decrypt those messages, so even the client that just encrypted them cannot read them anymore at this point.**
- The server receives those messages and, thanks to the private key it kept, can decrypt them.
## Creating synchronous encryption
Since asynchronous encryption like using a public/private key pair is a bit slow to use, **servers typically use them only to exchange a synchronous encryption key** that is then going to be used for all future communications.
This is how protocols such as HTTPS establish their communications and keep a fast rate of transfer going!
# Usage
- [[Transport Layer Security]]
- [[Secure Sockets Layer]]
- [[HTTPS]]
- Many, many more...
# Ressources
[Claude-generated Primer](https://claude.ai/share/cbddf3a4-f875-418d-ad44-855c20521b6c)