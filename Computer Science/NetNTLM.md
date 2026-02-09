---
tags:
---
NetNTLM is the legacy authentication protocol used on Windows machines.
# How it works
NetNTLM works **using a challenge-response mechanism**.
## Usual Authentication Workflow
![](https://tryhackme-images.s3.amazonaws.com/user-uploads/5ed5961c6276df568891c3ea/room-content/2eab5cacbd0d3e9dc9afb86169b711ec.png)
1. The client sends an authentication request to the server they want to access.
2. The server generates a random number and sends it as a challenge to the client.
3. The client combines their NTLM password hash with the challenge (and other known data) to generate a response to the challenge and sends it back to the server for verification.
4. The server forwards the challenge and the response to the Domain Controller for verification.
5. The domain controller uses the challenge to recalculate the response and compares it to the original response sent by the client. If they both match, then the client is authenticate.
6. The server forwards the authentication result to the client.
This way, **the password hash is never transmitted over the network**.