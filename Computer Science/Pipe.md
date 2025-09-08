---
tags:
  - low_level
---
Pipes are one-way communication tunnels taking the form of two [[File Descriptor]]s: one for writing into the pipe, and another one to read from it.
Usually, pipes are used for [[InterProcess Communication]], allowing two processes to send data via this one-way tunnel.