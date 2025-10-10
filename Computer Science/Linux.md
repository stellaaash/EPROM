---
tags: []
---
[[Unix]]
[[Window Manager]]
[[Login Manager]]
# Common Directories
- `/etc`: System/OS files.
- `/var`: Variable data, which is frequently accessed by services or apps running on the system for disk cache.
  Notable for storing logs in `/var/log`.
- `/root`: The home directory of the `root` user.
- `/tmp`: Temporary files that get wiped at shutdown.
# Namespaces
Linux uses **namespaces** to split up the resources available on a computer to processes.
They also help with security by compartmentalizing processes.