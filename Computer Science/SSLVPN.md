---
tags:
  - protocol
---
[[Secure Sockets Layer]] [[Virtual Private Network]] or SSLVPN is a remote access technology that enables secure connections to internal organizational ressources using SSL/TLS encryption.
It operates at the application and transport layers, which makes it work directly in standard web browsers or lightweight client software.
In other words, **it is a type of Virtual Private Network that uses SSL/TLS as its encryption layer**.
# How it works
SSLVPN operates **through an encrypted tunnel between a user's device and VPN gateway server**.
All traffic is encrypted using the SSL protocol or the newer [[Transport Layer Security]].
## Step by step
1. **Initial Connection**: Users point their browser at the SSL VPN gateway to initiate a handshake process.
2. **Server Authentication**: The gateway sends a certificate that the browser authenticates against trusted one or multiple [[Certificate Authority]].
3. **Encryption Negotiation**: The browser and server negotiate which encryption algorithm to use for securing the connection.
4. **Key Exchange**: Both parties exchange cryptographic keys to establish the encrypted tunnel through which all subsequent data flows.
# Why complicate VPNs even more?
The answer is pretty simple: **security**. You're encrypting all traffic going to and from the VPN for added security.
There are some notable advantages to SSLVPN specifically compared to other tradition [[IPsec]] solutions:
- **Browser-based Access**
- **Port 443 Compatibility**
- **Easy Client Deployment**
- **Flexible Network Access**
# Split vs Full Tunnelling
The difference between split tunnel and full tunnel in SSLVPN is how network traffic from the remote user is routed through the VPN:
- Full tunnel **routes all of the user's traffic, including local network access and internet browsing through the VPN**.
  This means that all data is encrypted and goes through the company's firewall.
  This provides maximum security and privacy, at the cost of latency and slower speeds on tasks that don't have to go through the company.
- Split tunnel, on the other hand, **routes only traffic destined for the internal company network or specific IP ranges** defined in the configuration.
  This improves speed and latency and reduces load on the VPN, but lowers privacy and security for the internet traffic that doesn't go through the tunnel.