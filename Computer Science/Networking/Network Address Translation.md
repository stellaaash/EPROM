---
tags:
---
Network Address Translation or NAT allows **using one public [[IP Address]] to access many private IP addresses**.
This addresses IPv4 address depletion by "hiding" entire networks behind a single public IP address.
# Keeping an address book
[[Router]]s that support NAT must keep a sort of address book of active connections, in order to figure out which goes to which host on its network.
Think about it: **a single public IP for 20 home devices. How do you determine which incoming packet goes where?**
As such, routers need to keep tally of all ongoing connections and especially which local host initiated them, so that it can effectively route the incoming packets to the right host.
# SNAT vs DNAT
Source NAT is when internal devices communicate with the internet: **the source IP address is translated and potentially also the port.**
This way, outgoing packets point back to the gateway doing the NAT translation, so it can find its way back on the wider network.
The opposite process happens in Destination NAT, when a packet is arriving at a NAT node: **the source IP address is translated to the actual device on the local network that wants it**. Same thing with the port.
The packet is then forwarded to that IP.
