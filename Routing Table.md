---
tags:
  - networking
---
A data table stored in a [[Router]] or other network host.
It contains information about the topology of the network directly around it.
# How it works
A routing table is a bit like a recipe, but in packet distribution.
It tells you for each destination you want to go to, **which target to send your package next**.
If the node cannot directly connect to the final destination of the packet, it has to send it via other nodes along a given route.
Each node along the way needs to keep track of which way to deliver packages of data.
For that, it uses a routing table.
## Hop-by-hop
By using hop-by-hop routing, where you give a packet to the next node in line for a destination,
it can effectively go from anywhere to anywhere else, so long as each node contains an entry for that destination.
Hop-by-hop is the fundamental characteristic of the [[IP]] Internet Layer and the [[OSI]] Network Layer.
## Attached networks
When a [[Router]] interface is configured with an [[IP Address]] and [[Subnet]] Mask, the interface becomes a host on that attached network.
A directly connected network is a network that is directly attached to one of the router interfaces.
## Direct networks vs Remote networks
The network address and subnet mask of the interface as well as its type and number are entered into the routing table as a directly connected network.
A remote network, on the other hand, is one that can only be reached by sending the packet to **another router**.
Routing table entries to remote networks can be either static or dynamic.
- Dynamic routes are routes that were learned automatically by the router through a dynamic routing protocol.
- Static routes are routes than a network admin manually configured.
# Structure
Usually, routing tables are databases that keep track of paths, like a map.
The network device uses these to determine which way to forward traffic when it is not the intended destination.
Most often, it is a file in RAM that is used to store route information about directly connected and remote networks.
Nodes can share the contents of their routing tables with other nodes.
# Resources
[Wikipedia](https://en.wikipedia.org/wiki/Routing_table)