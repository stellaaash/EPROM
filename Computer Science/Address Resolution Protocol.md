---
tags:
  - networking
---
ARP is a protocol **that allows devices to associate its [[MAC Address]] with an [[IP Address]] on the network**.
# How it works
## "Does anybody know this guy?"
Every device in a network stores a cache of other devices in the network, their MAC and IP addresses.
In order to associate the two, ARP uses two types of messages:
- **ARP Requests**: Broadcasts to the network, essentially asking **"What is the MAC address that owns this IP?**
- **ARP Replies**: When a device receives the ARP broadcast request, it can answers with its information (whether it actually owns that IP, or it knows someone who does).