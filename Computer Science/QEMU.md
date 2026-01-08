---
tags:
  - emulator
---
The Quick EMUlator, or QEMU, is a free and open-source emulator that uses dynamic [[Binary Translation]] to a emulate a computer's [[Processor]].
In doing this, it **translates the emulated binary codes to native binary code to be executed on the machine**.
QEMU supports the emulation of [[x86]], [[ARM]], [[PowerPC]], [[RISC-V]] and other architectures.
# Operating Modes
QEMU has **multiple operating modes**:
- **User-mode emulation**: runs single Linux or macOS programs that were compiled for a different target or [[Instruction Set]].
- **System Emulation**: emulates a full computer system, including its peripherals and hardware.
  Can be used to provide virtual hosting of several [[Virtual Machine]]s on a single computer.
- **Hypervisor support**: acts as either a Virtual Machine Manager or as a back-end for virtual machines running under a Hypervisor.
