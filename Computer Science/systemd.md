---
tags:
---
A **system and service manager for [[Linux]] [[Operating System]]s**.
It is usually run as the first [[Process]] (PID 1) as an init system that brings up and maintains user-space [[Service]]s.
Each logged in user has their own instance.
# How it works
## Starting up
systemd is usually installed as the `/sbin/init` [[Symbolic Link]] so that it's started during early boot.
When run as the system instance (not as a user's manager), it tries to read from the config file `system.conf` and all the files from the `system.conf.d` directories.
When run as a user instance, it interprets the `user.conf` and `user.conf.d` files and directories instead.[^1]
> **Extract from the systemd [[Linux]] manual :** systemd contains native implementations of various tasks that need to be executed as part of the boot process. For example, it sets the hostname or configures the loopback network device. It also sets up and mounts various API file systems, such as /sys/, /proc/, and /dev/.

Systemd also **resets the system clock during early boot if it is deemed to be incorrect**.

[^1]: systemd-system.conf(5)
## Units
systemd categorizes system resources into *units*, which may be in a number of *states*, which are defined below.
### Unit States

| State        | Description                                                                                                                                                                               |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| active       | Start, bound, plugged in... It all depends on the unit type.                                                                                                                              |
| inactive     | Stopped, unbound, unplugged... You get it.                                                                                                                                                |
| failed       | Similar to inactive, except that the unit itself *failed* in some way, like the process returning an error code, crashing, or timing out. Too many restarts also count as a unit failure. |
| activating   | Changing from active to inactive.                                                                                                                                                         |
| deactivating | Changing from inactive to active.                                                                                                                                                         |
| maintenance  | Unit is inactive and a maintenance operation is in progress.                                                                                                                              |
| reloading    | Unit is active and it is reloading its configuration.                                                                                                                                     |
| refreshing   | Unit is active and a new mount is being activated in its namespace (see [[Linux#Namespaces]].                                                                                             |
### Unit Types
For each of these types, **there exists an appropriate manual page**: `systemd.service(5)`, `systemd.socket(5)` etc...
1. **Service**: Start and control damons and the processes they consist of.
2. **Socket**: Encapsulate local IPC or network sockets in the system.
3. **Target**: Useful to group units, or provide well-known sync points during boot-up.
4. **Device**: Expose kernel devices in systemd.
5. **Mount**: Control mount points in the file system.
6. **Automount**: Provide automount capabilities, for on-demande mounting of filesystems.
7. **Timer**: Useful for triggering activation of other units based on timers.
8. **Swap**: Like mount units, except they encapsulate swap partitions or files in the [[Operating System]].
9. **Path**: Can be used to activate other services when file system objects change or are modified.
10. **Slice**: Used to group units which manage system processes, like services and Scope units.
11. **Scope**: Like services, except they manage process they haven't started by themselves.
Units are **defined by their configuration files**, which also names them.

> [!NOTE] Uncompleted research!
> Was reading section `UNITS` of `systemd(1)`.


# Configuring
The default configuration is set during compilation. All configuration found in system and user files and directories come to change that default config.
## Options
`DefaultLimitNOFILE` : Max number of file descriptors in processes launched by the `systemd` unit. Defaults to 1024:524288.