---
tags:
---
The Windows Registry is a **database containing all kinds of variables** that determine how Windows and applications run.
It is structured in *hives*, which are really just **binary files containing registry keys**.
## List of Hives
- `SYSTEM`: Services, Mounted Devices, Boot Configuration, Drivers, Hardware
- `SECURITY`: Local Security Policies and Audit Policy Settings
- `SOFTWARE`: Installed Programs, OS Version and miscellanous info, Autostarts, Program Settings
- `SAM` ([[Security Account Manager]]): Usernames and Metadata, Password Hashes, Group Memberships, Account Statuses
- `NTUSER.DAT`: Recent Files, User Prferences, User-Specific Autostarts
- `USRCLASS.DAT`: Shellbags, Jump Lists
