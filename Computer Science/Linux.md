---
tags: []
---
[[Unix]]
[[Window Manager]]
[[Login Manager]]
# Common Directories
- `/`: Root directory, the top level of the file system.
- `/home`: User home directories.
- `/bin`: Essential binary executables.
- `/sbin`: System administration binaries.
- `/etc`: Configuration files.
- `/var`: Variable data, which is frequently accessed by services or apps running on the system for disk cache.
  Notable for storing logs in `/var/log`.
- `/usr`: User programs and data.
- `/lib`: Shared libraries.
- `/root`: The home directory of the `root` user.
- `/tmp`: Temporary files. Cleared at every system shutdown, so useful to dump random stuff into.
# Namespaces
Linux uses **namespaces** to split up the resources available on a computer to processes.
They also help with security by compartmentalizing processes.