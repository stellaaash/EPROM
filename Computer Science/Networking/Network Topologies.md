---
tags:
---
In networking, **topologies refer to the way the network is mapped**, its design and structure.
There are multiple types of topologies out there. Here are some of the most notable ones:
# Star Topology
This topology features **all devices individually connected to a central device** (like a switch or hub).
It's one of the most straightforward topologies, because you just connect everything to a router and call it a day.
This means all information sent over this network transits by that single point.
## Advantages
- Easy to add new devices to the network
## Disadvantages
- Uses a lot of physical media (cables) and thus more expensive than other topologies out there
- Following the above point, also needs more maintenance than other models
- Single bottleneck, which means single point of failure
# Bus Topology
This type of connection is essentially **a single cable (backbone cable) to which all devices wire**.
It's a little like a tree branch: leafs (hosts) are attached to the branch (cable) which connects them to the tree (internet).
## Advantages
- Easy to set up and scale, you can simply add more devices by linking them to the cable
- Cost-efficient (only one cable for a multitude of hosts)
## Disadvantages
- Single bottleneck, which means single point of failure
- Can become quite slow if all hosts use the cable at the same time
- Hard troubleshooting because all devices talk on the same cable
# Ring Topology
Also known as token topology, it is similar to bus topology in the sense that all devices are connected directly to each other.
But instead of a single cable, **they form a loop, relaying information as it goes round around it.**
It's worth noting that devices relaying the data will prioritize their own before sending what others send them to relay through the loop.
Data goes in a single direction around the loop, either clockwise or counter-clockwise.
## Advantages
- Less dependence on a single point of failure
- Cheap, as not much cabling is required
- Easy to troubleshoot
## Disadvantages
- Inefficient when transmitting large amounts of data, because multiple relays have to be passed through
- Single point of failure : if one relay fails, a good chunk of the network is unable to communicate