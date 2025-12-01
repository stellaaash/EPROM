---
tags:
  - protocol
port: 161, 162
---
Simple Network Management Protocol or SNMP is an **Internet standard protocol** used for **collecting, organizing and managing information about devices** on [[Internet Protocol]] networks.
It operates on the application layer of the IP suite, and allows administrators to monitor network performance, detect faults and configure devices remotely.
SNMP uses a manager-agent model, where the manager monitors or manages devices running agent software that reports information back via SNMP.
It typically uses ports 161 for **requests** and 162 for **traps** (notifications).
# Main Components
## SNMP Manager
The **central monitoring system** (Network Management Station) that communicates with agents.
## SNMP Agent
Software that **runs on the machine to be monitored**, and sends data back to the manager.
## Management Information Base
The MIB is a hierarchical **database of variables** the agent exposes for monitoring and configuration.
SNMP managers query the MIB to obtain device status, performance metrics, configuration details, and receive alerts known as *traps*.
There exists *private MIBs* that are vendor-specific: **they create their own MIBs to allow people to monitor their devices more specifically**.
### Structure
It contains a collection of managed objects that **represent properties of network devices and services.**
MIBs are structured in a tree-like way, where the nodes represent various network elements or service attributes.
### OIDs
Each object has a unique Object Identifier, or OID, which allows to decide exactly what to monitor on which devices.
### Object Types
There are two main types of MIB objects: **scalar objects and tabular objects**.
The first **represent a single data point**, while the latter **are organized as tables representing repeated sets of related data, like network interfaces, for example**.
# Versions
There are three main version of SNMP. SNMPv3 enhances security by adding encryption, authentication and integrity checks.
SNMPv2 uses just community strings to determine what data is available, but anyone can listen to data if they have that string.