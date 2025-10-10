---
tags:
  - networking
---
Subnetting is the action of **splitting up a network into smaller, miniature networks within itself called subnets**.
It's a bit like having a network being a big cake. You slice it into smaller parts to share it between different people.
For a business, you might use it to have different networks for accounting, finance and HR, for example.
# How it works
Subnetting is achieved on the configuration level by **splitting the number of hosts that can fit in a network**.
You do this using a **subnet mask**. This becomes the section of an [[IP Address]] **that represents the network identifier**.
Any bits coming after the subnet mask will represent **the specific device connected to that subnet**.
## Cheatsheet

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
## The Rule of Three (I made it up)
There are three concepts common to all subnets out there (here, examples denote a network of `192.168.1.0/24`):
- The **network address**: This is the part of the IP address that identifies the start of the network itself. For example, `192.168.1.0`.
- The **host addresses**: These are addresses that are going to be handed out to the hosts connecting to the network. For example, `192.168.1.100`.
- The **default gateway**: This is the address that hosts are going to refer to if they need to send data **to another network**. For example, `192.168.1.254` (`.254` is the usual convention, along with `.1`).