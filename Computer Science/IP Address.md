---
tags:
  - networking
---
Every device using the [[Internet Protocol]] is assigned a unique IP address to distinguish them from others.
# Subnet mask
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
A 32-bit number divided into 4 blocks that go from 0 to 255.
Example : `192.168.1.1`
# IPv6

> [!NOTE] Research to be done!

# Reserved networks
Some networks are usually only used in cases of a private, internal network (your home wifi for example).
- `10.0.0.0` - `10.255.255.255`
- `172.16.0.0` - `172.31.255.255`
- `192.168.0.0` - `192.168.255.255`
They provide enough distinct addresses to be used without problems inside of a single, private network.
# Loopback addresses
There's a range of IP addresses specifically reserved for internal testing and communications within a single device.
This range is `127.0.0.0` - `127.255.255.255`.
The `127.0.0.1` is referred to as `localhost`, and represents the device itself.
# Private vs Public adresses
Private adresses are used on private networks like wifis and other home networks that aren't directly accessible from outside.
They are usually **assigned by the router**.
Public adresses, on the other hand, are **assigned by the ISP**, and provide a way to refer to a device on the entirety of the internet combined.