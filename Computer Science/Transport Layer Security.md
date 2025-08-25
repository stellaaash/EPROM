---
tags:
  - protocol
---
The TLS (Transport Layer Security) protocol is a cryptographic protocol designed to provide communications security over a network, like the Internet.
It's widely used for fields such as emails, instant messaging and VoIP, but its most known usage is in [[HTTPS]].
Its main purpose is to provide security, including privacy (confidentiality), integrity and authenticity.
# How it works
## Certificates and you
TLS (and [[Secure Sockets Layer]]) uses [[Certificates]]:
The server has to present a digital certificate proving that it is the intended destination for a packet.
The client, on the other hand, conducts the verification of the certificate, ensuring that:
- The subject of the certificate matches the [[Hostname]] (different from a [[Domain Name]]) to which the client is trying to connect.
- A trusted certificate authority has signed the certificate.

# Resources
[Wikipedia - Public Key Certificate]([Public key certificate - Wikipedia](https://en.wikipedia.org/wiki/Public_key_certificate))