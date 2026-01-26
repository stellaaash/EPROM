udev is a **userspace daemon that listens to the [[Linux]] [[Kernel]] for *uevents*, changes to the list of devices currently available to the system**.
Essentially, every time a new device gets plugged in, the kernel notifies udev through a uevent, and udev is charged with creating the userspace interface in `/dev/xxx` with the right permissions, thereby allowing the users to access the devices, too.
It is also tasked with **loading the appropriate [[Firmware]] for the devices** and creating symlinks referring to them.
# Types of Devices
## Block Devices
There are disks or partitions, addressable in blocks of space to write to.
## Character Devices
Those are the inputs and outputs: mice, keyboard, terminals, but also GPUs and audio outlets.
## Pseudo-devices
This is where it gets weird. The Linux kernel **provides abstractions for some features**.
- `/dev/null`
- `/dev/random`
- `/dev/zero`

# Configuration
udev stores its rules into `/usr/lib/udev/rules.d`.