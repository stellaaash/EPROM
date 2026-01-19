---
tags:
  - cryptography
  - networking
---
Digital Signatures or Certificates are **ways to confirm that data originates from a trusted source**.
They use asymmetric cryptography ([[Public-key Cryptography]]) to produce a signature using a private key, which can then be verified using a public key.
You essentially encrypt the plaintext with the private key, and then anyone can decrypt it using the public key to verify that the text does indeed match. If it doesn't, it means the data has been tampered with in some shape or form.
# Chain of Trust
Certificates have a so-called *chain of trust*, starting with a root *[[Certificate Authority]]*. Those are often trusted by devices in factory settings, and web browsers do the same.
Here's the thing: **certificates are trusted only when the root CA trusts the organization that issued the certificate**.