---
tags:
  - networking
  - protocol
---
The User Datagram Protocol or UDP is a *connectionless* Network layer protocol that is used to **communicate data between devices**.
Contrary to its brother [[Transmission Control Protocol]], UDP is **stateless**, which means that it **doesn't require a constant connection between two devices for data to be sent**.
The reason for this is simple: **no integrity is guaranteed**, data is just sent willy-nilly (sorta) and there's no confirmation that all of it has been received.
As such, UDP is faster, which makes it very useful for applications that tolerate packet loss, like video streaming or voice chat.
# UDP headers
- **Time To Live (TTL)**: Determines how long a packet can live on the network before expiring. This helps prevent clogging of the network.
- **Source Address**
- **Destination Address**
- **Source Port**
- **Destination Port**
- **Data**