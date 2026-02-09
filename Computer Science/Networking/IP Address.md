---
tags:
---
Every device using the [[Internet Protocol]] is assigned a unique IP address to distinguish them from others.
# Subnet Mask
IP addresses are "divided" into two parts, one identifies the network of the host, the other, the host itself.
In TCP/IP ([[Transmission Control Protocol]] over [[Internet Protocol]]), this is called the subnet mask.
The CIDR determines the number of 1-bits found in the subnet mask, and thus its size.
By using the CIDR, you can determine the number of subnets found in a network.
These are small independent networks; hosts need to be in the same subnet to communicate directly.

| CIDR | Dot-decimal     | IP-addresses per subnet | Usable IP-addresses per subnet | Number of subnets |
| ---- | --------------- | ----------------------- | ------------------------------ | ----------------- |
| /32  | 255.255.255.255 | 1                       | 0                              | 256               |
| /31  | 255.255.255.254 | 2                       | 0                              | 128               |
| /30  | 255.255.255.252 | 4                       | 2                              | 64                |
| /29  | 255.255.255.248 | 8                       | 6                              | 32                |
| /28  | 255.255.255.240 | 16                      | 14                             | 16                |
| /27  | 255.255.255.224 | 32                      | 30                             | 8                 |
| /26  | 255.255.255.192 | 64                      | 62                             | 4                 |
| /25  | 255.255.255.128 | 128                     | 126                            | 2                 |
| /24  | 255.255.255.0   | 256                     | 254                            | 1                 |
# IPv4
A 32-bit number divided into 4 octets that go from 0 to 255.
Example : `192.168.1.1`
# IPv6
IPv6 was born from the need to have a range much wider than the one available through IPv4.
It is **the latest version of the [[Internet Protocol]]**, and provides a **128-bit address space** ($3.4 \times 10^{38}$).
## Format
IPv6 addresses are 128 bits long and **are formatted as eight groups of 16 bits or 4 hexadecimal digits**.
The groups are separated by colons `:`. For example: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`.
Each group is called a *quartet* and can **omit zeros within the group**. For example, `0042` becomes `42`.
Consecutive groups of 0s can be compressed and replaced by a double colon `::`, but **this can only be used once per address to avoid ambiguity.**
As such, `2001:0db8:0000:0000:0000:0000:0000:0001` becomes `2001:db8::1`.
The prefix length is written after the address using a slash like `/64`, which is similar to IPv4's CIDR notation.
## Main Features
IPv6 simplifies packet headers for faster router processing, eliminates the need for IP fragmentation by hosts, and standardizes subnets at $2^{64}$ addresses for efficient routing.
It supports unicast, anycast and multicast transmission. Multicast **replaces IPv4's broadcast**.
As for security, built-in [[IPsec]] and improved mobility without triangular routing as well as [[Neighbor Discovery Protocol]] using [[Internet Control Message Protocol]] version 6 for address resolution instead of [[Address Resolution Protocol]].
# Reserved Networks
Some networks are usually only used in cases of a private, internal network (your home wifi for example).
- `10.0.0.0` - `10.255.255.255` (`10.0.0.0/8`)
- `172.16.0.0` - `172.31.255.255` (`172.16.0.0/12)
- `192.168.0.0` - `192.168.255.255` (`192.168.0.0/16`)
They provide enough distinct addresses to be used without problems inside of a single, private network.
These addresses cannot interact directly with the global network that is the internet, they have to go through a [[Router]] first to give it a public IP address.
# Loop Back Addresses
There's a range of IP addresses specifically reserved for internal testing and communications within a single device.
This range is `127.0.0.0` - `127.255.255.255`.
The `127.0.0.1` is referred to as `localhost`, and represents the device itself.
# Broadcast Address
In order to send a message to the entire network, you make your packet's target either the `255.255.255.255` address for an IPv4 network, or the **highest address of the subnet (all host bits set to 1)** for a subnet.
IPv6 does **not use broadcast addresses**. Instead, it uses *multicast addresses*.
# Private Vs Public Addresses
Private addresses are used on private networks like wifis and other home networks that aren't directly accessible from outside.
They are usually **assigned by the router**.
Public addresses, on the other hand, are **assigned by the ISP**, and provide a way to refer to a device on the entirety of the internet combined.
You very often **pay for the public IP address of your home network**- that's your bill (or a part of it, anyway)!