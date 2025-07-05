---
tags:
  - networking
  - hardware
---
A router is responsible for connecting multiple networks together.
It has multiple interfaces, usually one for each network it connects to.
# Network interfaces
Be careful to not make the ranges of [[IP Address]]es between interfaces overlap.
This would imply that the two interfaces belong to the same network.
# Routing Tables
Routers' primary job is to **forward traffic**.
To do so, they employ [[Routing Table]]s to send a packet towards its given destination.