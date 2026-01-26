chroot **changes what the current process believes is the root filesystem**.
# Syscall
At the syscall level, the C function is actually really really simple:
```c
int chroot(const char* path)
```
What it does internally is **modify a single pointer in your process' kernel data structure `fs_struct`, changing where the kernel believes `/` lies for that process**.
