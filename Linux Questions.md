## What is Linux?
- Linux is the open-source operating system based on the Linux kernel.
- It manages hardware and software resources.
- It is divided into 5 Subsystems :
- 1.Process management subsystem
- 2.Memory management subsystem
- 3.File management subsystem
- 4.Device driver management subsystem
- Network management subsystem.

## What is the difference between Linux and Windows OS?
### Linux :
- Linux is an open-source operating system built around the Linux kernel, supporting both hardware and software control.
- It allows customization and is commonly used in servers and embedded systems.
### Windows :
- Windows is a closed-source, paid operating system by Microsoft.
- It mainly designed for desktop and business use.

## What is the Linux kernel?
- The Linux kernel is the core part of the operating system that runs in kernel space.
- It manages hardware resources, system calls, memory, and processes, acting as a bridge between user programs and the hardware.

## What is a Linux Distribution?
- A Linux distribution is a complete version of the Linux operating system that includes the Linux kernel, libraries, utilities, and a package manager.
- Examples include Ubuntu, Fedora, Debian, and Kali Linux.

## What is the Linux Booting Process?
- The booting process is the sequence of steps that the Linux system performs from the moment you power it on until the login prompt or desktop appears.
- It basically takes your system from hardware → kernel → user space.
| **Stage** | **Name**                   | **What Happens**                                |
| --------- | -------------------------- | ----------------------------------------------- |
| 1️⃣       | **BIOS / UEFI**            | Hardware initialization                         |
| 2️⃣       | **MBR / GPT**              | Bootloader information is read                  |
| 3️⃣       | **Bootloader (GRUB)**      | Loads Linux kernel into memory                  |
| 4️⃣       | **Kernel Initialization**  | Kernel sets up hardware, mounts root filesystem |
| 5️⃣       | **init / systemd process** | Starts system services (background processes)   |
| 6️⃣       | **Login / Shell**          | User gets login screen or GUI                   |

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/f1ed4f39-50ca-48e0-a979-3d192f7811ad" />

