---
tags:
---
The TLS (Transport Layer Security) protocol is a cryptographic protocol **designed to provide communications security over a network**, like the Internet.
It's widely used for fields such as emails, instant messaging and VoIP, but its most known usage is in [[HTTPS]].
Its main purpose is to provide security, including privacy (confidentiality), integrity and authenticity.
# Certificates and you
TLS (and [[Secure Sockets Layer]]) uses [[Certificates]]:
The server has to present a digital certificate proving that it is the intended destination for a packet.
The client, on the other hand, conducts the verification of the certificate, ensuring that:
- The subject of the certificate matches the [[Hostname]] (different from a [[Domain Name]]) to which the client is trying to connect.
- A trusted certificate authority has signed the certificate.
The *Subject* field of the certificate must identify the primary hostname of the server as the *Common Name*.
The hostname **must be publicly accessible**, as in not using private addresses or [[Reserved Domain]].
A certificate may be valid for multiple hostnames, for example if a domain has multiple subdomains.
Some certificates are called **wildcard certificates** because they contain a `*` to target multiple subdomains.
Public-facing servers must obtain their certificates from a **trusted and public [[Certificate Authority]] or CA**.
## Not just servers!
There are also TLS/SSL **client** certificates, authenticating a host connecting to a TLS service.
These certificates usually contain an email address or personal name instead of a hostname.
Client certificates are common in [[Virtual Private Network]]s and [[Remote Desktop Services]], where they authenticate devices.
___
There are also email certificates, establishing **message integrity and encrypting said messages**.
## Self-signed certificates, or how to DIY the thing
A self-signed certificate is a certificate that has a subject matching its issuer, effectively the issuer certifying itself.
Of course, these are worthless to attest that someone is trustworthy (we have examined ourselves and found no fault of our own), especially in remote communications.
# Resources
[Public key certificate - Wikipedia](https://en.wikipedia.org/wiki/Public_key_certificate)