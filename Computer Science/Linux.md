---
tags: []
---
[[Unix]]
[[Window Manager]]
[[Display Manager]]
# Common Directories
- `/`: Root directory, the top level of the file system.
- `/home`: User home directories.
- `/dev`: System devices exposed by [[udev]].
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
## How??
The [[Kernel]] itself is responsible for enforcing the separation between namespaces.
For all the namespaces listed below, each process has a reference to one (several processes could share on `net` namespace, for example), dictating what resources they have access to.
This is how [[Docker]] containers don't have access to other processes: **they have a separate `pid` namespace as the rest of the system**.

> [!WARNING] Namespaces aren't copied!
> Be careful not to create a mental image of each process copying the parent's namespaces. **It is the kernel which manages namespaces**.
> It assigns every process its namespaces (one for each that exists), and enforces those rules when receiving syscalls.
> If a process belonging to a `pid` namespace with only itself tries to get the list of PIDs from the kernel, the kernel will tell the process that it is PID 1, the sole process in that namespace.
> This effectively **creates isolation**, as the process isn't even aware of the existence of others. To it, **it is the first process that was started on the system**.

## List of modern Linux Namespaces
- `mnt`: Mount points
- `pid`: Process ID number space
- `net`: Network stack (interfaces, routing tables, [[iptables]])
- `uts`: Hostname and domain name
- `ipc`: [[System V]] [[InterProcess Communication]], [[POSIX]] message queues
- `user`: User/group ID mappings
- `cgroup`: Cgroup root directory view