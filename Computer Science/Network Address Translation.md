---
tags:
  - networking
---
Network Address Translation or NAT allows **using one public [[IP Address]] to access many private IP addresses**.
This addresses IPv4 address depletion by "hiding" entire networks behind a single public IP address.
# How it works
## Keeping an address book
[[Router]]s that support NAT must keep a sort of address book of active connections, in order to figure out which goes to which host on its network.
Think about it: **a single public IP for 20 home devices. How do you determine which incoming packet goes where?**
As such, routers need to keep tally of all ongoing connections and especially which local host initiated them, so that it can effectively route the incoming packets to the right host.