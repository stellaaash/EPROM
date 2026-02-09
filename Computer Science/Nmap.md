---
tags:
---
Nmap is **an open-source network scanner**.
# Cheat sheet
Nmap specifies its targets multiple ways:
- Using an IP range with`-`, for example `nmap 192.168.0.1-10` to scan all 10 [[IP Address]]es in this range
- Using an IP [[Subnet]] with `/`, for example `nmap 192.168.0.1/24` to scan all IPs in the subnet
- Using a hostname, for example `nmap google.com`
```bash
nmap 192.168.0.1

# Basic syntax
nmap 192.168.0.1-10  # Scan all IP 10 addresses within that range
nmap 192.168.0.1/24  # Scan all IP addresses withing the specified subnet
nmap google.com  # Use a hostname directly
nmap 8.8.8.8 -v  # Enable verbose output
nmap 8.8.8.8 -vv
nmap 8.8.8.8 -vvv
nmap 8.8.8.8 -vvvv
nmap 8.8.8.8 -d  # Enable debug output. There are multiple levels, with the max being -d9

# Basic scans
nmap -sn 8.8.8.8  # Ping scan
nmap -sL 192.168.0.1/24  # Lists the targets to scan without actually scanning them
nmap -sS -Pn 8.8.8.8  # Treat all hosts as online (still scan even if they seem down)

# Port enumeration
nmap -sT 8.8.8.8  # Connect scan - attempt the three-way handshake with every target port
nmap -sS 8.8.8.8  # SYN scan - send only the TCP SYNc request without actually establishing a connection
nmap -sU 8.8.8.8  # Scan for UDP services
nmap -sT -F 8.8.8.8  # Fast mode, only scans the 100 most common ports
nmap -sT -p10-1024 8.8.8.8  # Define a range of ports to scan for (from port 10 to port 1024)
nmap -sT -p-25 8.8.8.8  # Define a range of ports to scan for (from port 1 to port 25)
nmap -sT -p- 8.8.8.8  # Define a range of ports to scan for (from port 1 to port 65535)

# Version detection
nmap -sS -O 8.8.8.8  # Enable OS detection
nmap -sS -sV 8.8.8.8  # Enable service and version detection
nmap -A 8.8.8.8  # Enable both OS and service and version detection

# Saving output
nmap -sT -oN wow.nmap 8.8.8.8  # All output to a file
nmap -sT -oX wow.nmap 8.8.8.8  # XML output to a file
nmap -sT -oG wow.nmap 8.8.8.8  # grep-able output
nmap -sT -oA wow 8.8.8.8  # Output in all major formats to a file (no need for an extention as multiple files will be created)
```
## Scanning speeds
Since scanning too fast might trigger automatic or manual securities (like an [[Intrusion Detection System]] or equivalent), it might be best to manually set the speed at which nmap scans.
Nmap provides six templates:
- 0 - Paranoid
- 1 - Sneaky
- 2 - Polite
- 3 - Normal
- 4 - Aggressive
- 5 - insane
```bash
# Paranoid examples
nmap -sT -T0 8.8.8.8
nmap -sT -T 0 8.8.8.8 
nmap -sT -T paranoid 8.8.8.8 
```
## Parallel probes
Also affecting the scanning speed is the **number of parallel service probes**.
You can control those with the `--min-parallelism` and `--max-parallelism` flags.
By default, nmap looks at the connection quality to determine how much probes it can have running at the same time.
## Packet rate
Similarly, the `--min-rate` and `--max-rate` flags allow to set a rate at which the packets are to be sent.
The rate is provided **as the number of packets per second**.
## Host Timeout
The `--host-timeout` flag allows to set how long we should wait on a service before timing out.