---
tags:
---
When a [[Router]] sends an [[Internet Protocol]] packet on its way to its destination, it can use a variety of **routing protocols** to choose which path to take.
# OSPF - Open Shortest Path First
This protocol allows routers to share information about the network topology and calculate **the most efficient path for transmission**.
It does this by having routers exchange updates about the state of their connected links and networks.
This way, **each router has a complete map of the network and knows which route to send the packet to for fastest arrival**.
# EIGRP - Enhanced Interior Gateway Routing Protocol
A [[Cisco]] proprietary protocol that combines many aspects of different routing algorithms.
It allows routers to share info about the networks they can reach **and the cost like bandwidth or delay**.
Routers then use this information to use the best path.
# BGP - Border Gateway Protocol
The primary routing protocol used on the Internet.
It allows different networks (like those of [[Internet Service Provider]]s) to exchange routing information and establish paths for data to travel between those networks.
# RIP - Routing Information Protocol
A simple routing protocol, it is often used in small networks.
Routers running RIP share information about the networks they can reach and the number of hops (routers) to reach them.
As a result, each router builds a [[Routing Table]] based on this information, and chooses the route with the least amount of hops.