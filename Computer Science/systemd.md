---
tags:
  - Linux
---
A **system and service manager for [[Linux]] [[Operating System]]s**.
It is usually run as the first [[Process]] as an init system that brings up and maintains user-space [[Service]]s.
Each logged in user has their own instance.
# How it works
systemd is usually installed as the `/sbin/init` [[Symbolic Link]] so that it's started during early boot.
When run as the system instance (not as a user's manager), it tries to read from the config file `system.conf` and all the files from the `system.conf.d` directories.
When run as a user instance, it interprets the `user.conf` and `user.conf.d` files and directories instead.[^1]
> **Extract from the systemd [[Linux]] manual :** systemd contains native implementations of various tasks that need to be executed as part of the boot process. For example, it sets the hostname or configures the loopback network device. It also sets up and mounts various API file systems, such as /sys/, /proc/, and /dev/.

[^1]: man 5 systemd-system.conf(5) on a [[Linux]] system for more info.

# Configuring
The default configuration is set during compilation. All configuration found in system and user files and directories come to change that default config.
## Options
`DefaultLimitNOFILE` : Max number of file descriptors in processes launched by the `systemd` unit. Defaults to 1024:524288.