---
tags:
  - networking
---
A firewall is a hardware or software utility that **filters incoming and outcoming connections for a device of network**.
Firewalls are powerful tools, able to be configured to let in or out connections based on a number of factors, such as traffic target and origin, ports and protocols.
They inspect the packets being transmitted to check if they follow the rules set in place by the network admin.
# Types of firewalls
## Stateful
This type of firewall **looks at the connection information rather than individual packets** to determine if a connection is allowed or not.
Consumes a lot of ressources, since the decision making is dynamic on the entire connection.
It blocks the entire incoming device if it asserts that one of its connections is bad.
## Stateless
Stateless firewalls are much simpler than stateful ones, as **they only check individual packets for a list of static rules**.
As such, they do not block entire devices if one of their packets is bad; which makes them less robust than stateful firewalls. However, they also take way less ressources to run.
If a rule isn't *exactly* matching a packet, it will go through.
# Network Zones
Also called *security zones* or *firewall zones*, they **help segment networks and apply different security policies based on trust levels**.
## Examples of Network Zones
### Local Area Network - LAN
Internal, trusted network for devices like computers, servers and printers within an organization.
High trust level with permissive rules allowing internal communication and outbound internet access.
### Wide Area Network - WAN
External, untrusted network typically representing the internet or [[Internet Service Provider]] connection.
Lowest trust level with strict inbound restrictions to block unauthorized access.
### DeMilitarized Zone - DMZ
Semi-trusted buffer network for public-facing servers, for example web, email, ftp, dns...
Isolated from the LAN to limit breach impact.
### [[Virtual Private Network]] - VPN
A special zone for remote users. Usually directly connected to the LAN to allow for access to local resources from remote locations.
# Examples of firewalls
- [[Snort]]