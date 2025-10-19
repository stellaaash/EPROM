---
tags:
  - networking
---
A **physical network interface's identifier**, the MAC (Media Access Control) address is here to uniquely identify a physical device.
These can range from microchips found on motherboards, to interfaces found on database servers.
All network devices are assigned a MAC address. These are hardcoded in the Network Interface Card or NIC, and thus cannot be changed.
# Structure
MAC addresses are composed of **hexadecimal numbers**, 12 characters in total.
Example: `a4:c3:f0:85:ac:2d`
The first six characters **identity the company that made the network interface**.
The last six is a unique number to identify the interface among all others made by the same brand.
# Broadcast address
Like for [[IP Address]]es, MAC addresses have a special **broadcast address set to `ff::ff::ff::ff::ff::ff`**.
This is used for network wide broadcasting and communications, like like [[Address Resolution Protocol]] requests, network discovery and management tasks.
# Spoofing
When communicating on a network, **MAC addresses of devices can be spoofed**.