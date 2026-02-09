---
tags:
---
A reverse proxy is **a server that sits in from of [[Web Server]]s and forwards client requests to those web servers**.
This helps in increasing security, performance, and reliability of the information presented by the web servers.
# Isn't that the Same as Forward Proxies?
Contrary to a [[Web Proxy]] or forward proxy, a Reverse Proxy sits in front of the servers, not the clients.
This means the protection that the proxy provides is given to the servers, not the clients. This gives different advantages:
- **[[Distributed Denial of Service]] protection**
- **Load Balancing**, where traffic is distributed on multiple servers serving the same page
- **General protection from attacks**, as web servers don't have to expose their real [[IP Address]] that way
- **Caching**
- **SSL/TLS Encryption**, something that is expensive for an origin server