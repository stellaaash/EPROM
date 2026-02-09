---
tags:
---
The OSI model (Open Systems Interconnection Model) is an **essential model used in networking**.
It **provides a framework dictating how all networked devices will communicate**.
It exists primarily to allow devices to have different functions and designs, and setting a standard for how devices will talk to each other on a network.
It has seven layers, each of which has a different **set of responsibilities** and is arranged from Layer 7 to Layer 1.
You start at level 7 with your application, and **wrap each layer in a new one as you go up the layers until the physical media**.
# Layers, or how the internet really is just an onion
The Layers of the OSI model allow for **encapsulation of the processes happening at different levels of network communications**.
For example, it helps define the limit between the physical communications happening (the actual electricity), and the more software-defined protocols in place.
## 1. Physical
This layer represents the **actual physical media you wire between devices**. It doesn't get any lower level than that!
On this layer, you find the individual electrical signals representing the 1s and 0s of the world.
Supporting media can be standard ethernet cables, or wireless waves, or light signals in fiber optics, among others.
## 2. Data link
The Data link layer focuses on the **physical addressing of the transmission**.
When it receives a packet from the Network layer, it adds in the [[MAC Address]] of the receiving host to create a *frame*.
In all network-enable devices, there is a **Network Interface Card or NIC** that comes with a unique MAC address identifying it among all others.
When information is sent across a network, it is **actually primarily the MAC address that identifies the destination host**.
## 3. Network
Here, **routing and re-assembly of data** both take place.
It is at this layer that [[IP Address]]es enter the picture, and are used to route packets.
Devices like [[Router]]s are known as **Layer 3 devices** because they operate on the third layer.
### Routing
This process **determines the optimal path to send a packet to**, given a destination host.
Several protocol can take charge of routing at the Network layer, including but not limited to [[Open Shortest Path First]] and [[Routing Information Protocol]].
Multiple factors are taken into account when routing, such as:
- Distance: The number of devices that the packet needs to travel through
- Reliability: The paths that have the least packet loss
- Speed: The rate at which information can be sent on each path
Also see [[Routing Table]].
## 4. Transport
This layer, while more abstract, plays an essential role in the overall transmission of data over a network.
The *port* that the connection or packet uses is specified here.
When data is sent between devices, it follows one of two protocols: [[Transmission Control Protocol]] or [[User Datagram Protocol]].
Here is a brief comparison of both:

|                     | TCP<br>                    | UDP                  |
| ------------------- | -------------------------- | -------------------- |
| Concept             | Reliability and guarantees | Simplicity and speed |
| Error checking      | Yes                        | No                   |
| Reserved connection | Yes                        | No                   |
| Speed               | Slower                     | Faster               |
- TCP will **guarantee the integrity of all data** that is being sent by asking for confirmation, something UDP does away with for the sake of speed.
- TCP will make sure that both communicating entities **aren't being flooded by too many requests**, and throttles the speed of transmission if needed.
  UDP, on the other hand, lets the ***application layer*** **decide the speed of transmission**, allowing for much more flexibility.
UDP is particularly useful for transmission of **small pieces of data or larger files like for video streaming**; this is the case because, in such applications, **a small percentage of packet loss may be acceptable** (occasional pixelated videos, for example).
Other protocols using UDP include [[Address Resolution Protocol]] and [[Dynamic Host Configuration Protocol]].
## 5. Session
Once data has been formatted and prepared by the above Presentation layer, the Session layer will **initiate and maintain the connection to a host**.
When a connection is established, **a session is created, and it stays as long as the connection stays active**.
This layer is also responsible for closing the connection once all packets have been transmitted.
A session can also contain **checkpoints**, which allow for bandwidth saving when packets have been lost on the way, by only sending the newer packets.
Sessions are **unique**, and data cannot travel through multiple sessions from one host to another.
## 6. Presentation
This is the layer in which standardization takes place: the application layer data will be wrapped in a way that can be used by all network devices.
This is important, since all applications work in different ways, and must then be standardized when sent over the network.
This layer thus **acts as a translation layer for data from the application layer**.
Security features like **data encryption** occur at this layer.
## 7. Application
This layer is the layer that's the closest to the user, and thus the one they interact the most with. **It defines how they should interact with data sent or received**.
Applications and interfaces are created in order to help the user interface with the network, for example when using a mail client or a web browser.
# Packets, frames and encapsulation
## Nicely wrapping data - Encapsulation
Packets and Frames are important concepts in the OSI model, both **representing fragments of data but at different levels** of the model.
Packets are represented at layer 3, containing an IP header and payload.
Frames, however, are used at layer 2, containing a MAC address (among other information) and the payload.
Think of it like an onion: **the center layer is the real data, and as it up the layers, more layers of information get added onto it to facilitate routing to its final destination**.
This is why Data Link adds a MAC address, and the Network layer adds an IP header. Each layer adds information that it is going to use to send the packet on its way. In the analogy, you can think of the Data Link as an envelope, and the Network layer as a cardboard packet (see what I did there?).
**This process is called encapsulation**.
## Okay but... why?
Frames and packets especially **both serve to make transmission of data easier and faster**.
Rather than sending the entire piece of data at once, it is broken down into smaller frames that then get wrapped as packets and sent over the network thanks to the IP and MAC information attached.
## Some notable headers of packets
- **Time to Live**: This fields sets an expiry timer for the packet, in order to prevent it from clogging the network should it get stuck in transit.
- **Checksum**: This field provides integrity checking for protocols like [[Transmission Control Protocol]]. If data is altered on the way, this value will be different that what is expected, and will flag the packet as being corrupt.
- **Source Address**: Pretty self explanatory, helps to send back information when receiving the packet, especially for TCP.
- **Destination Address**: Simple as well, sets the IP the packet should be forwarded towards.