---
tags:
  - protocol
---
Dynamic Host Configuration Protocol or DHCP is a network protocol for configuring [[Internet Protocol]] hosts with [[IP Address]]es, IP prefixes and other networking configuration data.
It aims to solve the problem of every device taking a random IP, leading to overlaps and conflicts of addresses on larger networks.
It runs on [[User Datagram Protocol]] on port 67 for the server and 68 for the client.
# How it works
## First connecting
When a device first connects to a network, **it broadcasts a message searching for a DHCP server**, a DHCP *Discover* broadcast.
Any DHCP server that might hear it on the local network will then **answer with an DHCP *Offer***, containing an IP address and the other **network configuration the new host needs**.
The device might have received several requests from multiple DHCP server, so it will choose one, and answer back to confirm the new IP address (DHCP *Request*).
Finally, the DHCP server sends a final acknowledgement (*ACK*) confirming the new configuration; the new device can now use the IP address for a specified period of time.
## Renewal of addresses
Rather than giving out addresses permanently, each device is given a "**lease**".
Each IP address comes with lease time configured on the DHCP server.
This way, if devices connect once and then stop connecting for a long time, their assigned IP address can be reused for someone else.
Of course, devices that keep connecting **can renew their lease** of their given address, usually around 50% of the lease time.
If that fails, it tries again at around 87.5% of the lease time. If it fails again, it starts the whole process over again (announcing itself to find a new DHCP server).
## Spread of configuration
Thanks to the lease system, **changes in configuration will gradually be distributed to all devices** that use DHCP.
This way, you don't have to go update each device's configuration manually.
And thanks to DHCP's wide range of possible broadcast information, **you can easily update your whole network's configuration by just changing what DHCP sends over**.
## Scopes and Pools
DHCP servers work with scopes or pools: **predefined ranges of address that are available for assignment**.
System administrators can also configure **reservations** within pools in order for specific devices to always get the same IP address.
The server keeps track of who has what address, how many addresses are available, reserved, etc.
It's like a hotel reservation system, but instead of rooms, it's IP addresses.
## More than just IP addresses
While IP address assignment is DHCP's main job, it's technically just a general-purpose configuration delivery system.
It delivers [[Subnet]] mask, default gateway and [[Domain Name System]] server addresses information along with the assigned [[IP address]].
As such, it can also deliver **dozens of other information** configurable on the server:
- Time server addresses
- Boot server locations for network-based operating systems
- Many, many more...
