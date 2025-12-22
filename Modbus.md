---
tags:
port: "502"
---
A protocol **without authentication to manage [[SCADA]] systems** and other industrial devices.
It is still widely used today despite its age because of its **simplicity, reliability and ease of use**.
# Data Types
Modbus organizes data into **four distinct types**, each serving a specific purpose in automation:
- Coils: binary values representing an output (valve open, motor running, alarm active)
- Discrete Inputs: binary values representing sensor input (button pressed, door closed, sensor triggered)
- Holding Registers: analog outputs, from 0 to 65535
- Input Registers: analog inputs, from 0 to 65535
# TCP vs Serial
Modbus was original created to work over serial cables, but **it can now also use [[Transmission Control Protocol]] for its transport layer**.