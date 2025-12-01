---
tags:
  - networking
---
A VPN or Virtual Private Network is a way to **create a dedicated tunnel between two network or devices, effectively creating a new network** (hence the name).
This allows devices from different geographical positions to be connected together regardless of distance (or network!).
# Okay, but... why?
Using a VPN has multiple benefits:
- It allows networks in **different geographical locations to be connected**.
  For example, a business with multiple offices worldwide will find it very beneficial when using it to create a single, interconnected network.
  It's also useful for remote workers to bypass external firewall rules when working on the goal.
- It offers privacy. VPN technology **uses encryption to protect data sent through the tunnel**.
  This prevents the packets to be intercepted by a third party, which makes VPNs very very useful on public networks and to bypass router-specific rules (in which the router checks where packets are sent).
- It offer anonymity.
  Using a VPN effectively **helps at hiding your identity**, which is very useful for journalists and activists in countries where censorship is rampant.
  Of course, anonymity depends on the level of logging performed by the VPN's other devices. As such, only use VPNs from trusted sources (or your own).
# VPN technologies
There are several major VPN protocol versions, each using a different way to encrypt the actual data being transmitted.
## PPP
This is used by PPTP to allow for authentication and provide encryption of data.
VPNs work by using a private key and public certificate, a bit like [[Secure SHell]] (see [[Public-key Cryptography]]).
This technology is not capable of leaving a network by itself (non-routable).
## PPTP
The **Point-to-Point Tunneling Protocol or PPTP** is the technology that allows the data from PPP to **travel and leave a network**.
 It is very easy to setup and supported by most devices, but is weakly encrypted compared to alternatives.
> [!ERROR] Warning
> **Older protocol; should be avoid for real-world usage.**
## IPSec
**Internet Protocol Security or IPSec** encrypts data using the IP framework.
It's more difficult to set up, but is way stronger in encryption and is also widely supported.
Typically uses AES for encryption.
## OpenVPN
Uses the SSL/TLS protocol for key exchange and control, and then AES (often AES-256) for encrypting the actual data.
Highly flexible and secure, works at the transport layer.
## WireGuard
A newer protocol that uses the ChaCha20 cipher for encryption.
Simpler and faster, with a modern cryptographic design.
## SSTP
Secure Socket Tunneling Protocol uses SSL/TLS over port 443 to bypass firewall and provide strong encryption.
Mainly used on Windows boxes.
## [[SSLVPN]]
This one uses plain SSL/TLS as the encryption layer for the VPN connection.