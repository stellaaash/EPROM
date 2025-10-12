---
tags:
  - Windows
---
A Windows Domain is a **group of hosts under the administration of a given business**.
The idea of a domain is to facilitate administration of multiple hosts under a single hat called the *Active Directory*.
The server that runs the Active Directory services is called the *Domain Controller*.
# Advantages
- Centralized management of users
- Easy management of security policies for users and computers
- You can log in as your Active Directory user on all machines under the domain.
# Domain Controller
The Domain Controller **enforces the users and hosts under the domain**.
It populates user and security policies and takes care of authentication: when you try to log in as an Active Directory user, the host queries the Domain Controller to check for credentials.
*Policies* allow to restrict what access each type of user has (settings, windows updates and more).
# Objects
The Active Directory Domain Service or ADDS stores all objects of the AD domain it manages.
These contain:
- **Users**: Individual user accounts. They are part of the *Security Principals* - objects that have power over network devices such as hosts, printers and the like.
  Users can be represented as two types of entities: *people* and *services*. Indeed, you can also define users to be used by services like databases or web servers.
- **Machines**: Every computer joining the Active Directory. Machines are also *Security Principals*.
  They are also assigned an account, though a limited one within the domain itself (local administrators but not much rights on the domain).
  These accounts aren't meant to be logged in, but you can. These are named with the name of the machine followed by a dollar sign.
- **Security Groups**: Groups of users with specific permissions and access rights.
  These are also *Security Principals*, and as such can have privileges over resources on the network.
  Groups can have both users and machines as members, or even other groups as well.
  Several *Security Groups* are created by default in a domain.
## Organizational Units
In Windows Domains, objects are often organized using *organizational units or OUs*.
These often represent individual departments in a business, or even physical locations.
They mimic the actual organizational structure of the company.
**Each user can only be part of one OU at a time**.
Security Groups are used for **applying permissions over ressources**, while OUs are used to **apply policies** to users and computers.
# Group Policy Objects
Group Policy Objects or GPOs are **collections of settings that can be applied to Organizational Units**.