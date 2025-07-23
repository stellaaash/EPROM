---
tags:
  - adminsys
---
Fail2Ban is an **intrusion prevention software framework**, designed to **prevent brute-force attacks**.
It can run on any [[POSIX]] system that has a packet-control system or [[Firewall]] installed, like [[iptables]].
# How it works
It operates by monitoring log files for specific entries that were configured.
Most often, Fail2Ban is configured to block (ban) specific [[IP Address]]es that might be trying to breach system security.
For example, it can ban any host IP that makes too many login attempts, or does some other unwanted action.
It can **perform actions** when an IP is banned, like updating firewall rules or other tools to reject that IP's connections entirely.
# Resources
[Fail2ban - Wikipedia](https://en.wikipedia.org/wiki/Fail2ban)