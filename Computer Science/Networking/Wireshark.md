---
tags:
---
Wireshark is a **packet analyzer tool capable of sniffing internet traffic and inspecting packet captures**.
# Filter Queries
There are two types of filters in Wireshark:
- **Capture Filters**: This filter is set before capturing and **is used to save only a specific part of the traffic**. It cannot be changed once capturing starts.
- **Display Filters**: This filter **is used to reduce the number of visible packets**. It is changeable during and after capture.
## Capture Filter syntax
These filters pture Filter Syntax
These filters use byte offsets hex values and masks with boolean operators, so it's pretty convoluted.
Quick references cause I'm lazy and probably not going to use them as much: [1](https://www.wireshark.org/docs/man-pages/pcap-filter.html) and [2](https://gitlab.com/wireshark/wireshark/-/wikis/CaptureFilters#useful-filters)
## Display Filter Syntax
Probably Wireshark's most powerful feature. So much so that there is an [Official Display Filter Reference](https://www.wireshark.org/docs/dfref/) to refer to.
There's even a quick reference available directly in Wireshark under `Analyse -> Display Filters`.
Some samples:
```c
tcp.port == 80  // Display only traffic on port 80
ip.src == 10.10.10.100  // Display only traffic that contain the IP Address as destination or source
ip.src != 10.10.10.100  // Display all traffic that doesn't contain the IP as destination or source
ip.ttl > 250  // Display only packets with TTL values above 250
ip.ttl < 10  // Display only packets with TTL values below 10
ip.ttl >= 250  // Display only packets with TTL values above or equal to 250
ip.ttl <= 10  // Display only packets with TTL values below or equal to 10

# Some advanced stuff
http.server contains "Apache"  // Checks that a string contains a substring (case-sensitive)
http.host matches "\.(php|html)"  // Checks for matches to a regex
tcp.port in {80 443 8080}  // Checks if a value is contained in a specific scope/range
upper(http.server) contains "APACHE"  // Converts a field to uppercase then compares it
lower(http.server) contains "apache"  // Converts a field to lowercase then compares it
string(frame.number) matches "[13579]$"  // Converts a non-string value to a string

```

> [!NOTE] 
Wireshark supports both decimal and hex values in filtering.
You can also combine filters with `&&`, `||` and `!`.

