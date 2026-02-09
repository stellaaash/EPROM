---
tags:
---
tcpdump and its C/C++ library `libpcap` are widely used to analyze network traffic.
The library in particular is used in many other software to power their features.
# Cheat sheet
## Most important flags
```bash
tcpdump -i any  # Listen on all interfaces
tcpdump -i eth0  # Listen only on eth0
tcpdump -i eth0 -c 900  # Only capture 900 packets before ending
tcpdump -i eth0 -n  # Disable DNS lookups
tcpdump -i eth0 -nn  # Disable DNS lookups and port number lookups
tcpdump -i eth0 -v  # Enable verbose output
tcpdump -i eth0 -vv  # Enable more verbose output
tcpdump -i eth0 -vvv  # Enable even more verbose output

tcpdump -i any -w wow.pcap  # Saves traffic to a file named wow.pcap (.pcap is the norm for packet captures)
tcpdump -r wow.pcap  # Reads traffic from a saved pcap file

# Output formatting
tcpdump -i any -q  # Quick output, print brief packet information
tcpdump -i any -e  # Print the link-level header
tcpdump -i any -A  # Show packet data in ASCII
tcpdump -i any -xx  # Show packet data in hex format
tcpdump -i any -X  # Show packet headers AND data in hex and ASCII
```
## Filtering
It might be beneficial to check `man pcap-filter`.
```bash
# Filtering by host
tcpdump host google.com -i any  # Capture only traffic from host google.com
tcpdump host 8.8.8.8 -i any  # Capture only traffic from host with IP address 8.8.8.8

# Filtering by port
tcpdump host google.com port 80 -i any  # Capture only traffic from host google.com on port 80
tcpdump host google.com src port 80 -i any
tcpdump host google.com dst port 80 -i any

# Filtering by protocol
tcpdump -i eth0 icmp -n  # Capture only traffic that uses the ICMP protocol.

# Filtering by TCP Flags
tcpdump "tcp[tcpflags] == tcp-syn"  # Capture only packets that have the SYN flag set
tcpdump "tcp[tcpflags] & tcp-syn != 0"  # Capture only packets that have AT LEAST the SYN flag set
tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"  # Capture only packets that have AT LEAST EITHER the SYN or the ACK flag set

# Filtering by size
tcpdump -i eth0 greater 7000  # Capture only packets above 7000 bytes in length
tcpdump -i eth0 less 7000  # Capture only packets below 7000 bytes in length
```
## Logical Operators
```bash
tcpdump host 1.1.1.1 and tcp  # Captures tcp traffic with host 1.1.1.1
tcpdump udp or tcp  # Captures both tcp and udp traffic
tcpdump not tcp  # Captures all packets except tcp segements (would result in udp, icmp and arp packets)
```