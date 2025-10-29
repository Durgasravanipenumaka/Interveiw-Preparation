# Yocto :

- Yocto is not an operating system. It is a build system or framework used to create custom Linux distributions for embedded systems (like boards, IoT devices, routers, automotive systems, etc.).
- Yocto helps you build your own version of Linux — specifically designed for your embedded hardware.

---

## What Yocto Actually Does

> Yocto automates building all parts of an embedded Linux system.

| Component                    | Yocto Role                                       |
| ----------------------------- | ------------------------------------------------ |
| **Bootloader**               | Builds U-Boot or other loaders                   |
| **Linux Kernel**             | Builds custom kernel with selected configuration |
| **Root Filesystem**          | Builds minimal or full Linux file system         |
| **Applications & Libraries** | Builds your chosen software packages             |
| **Image Generation**         | Produces flashable `.img` or `.tar.gz` files     |

---

## Yocto is Based On BitBake :

- Yocto’s build engine is called **BitBake** — it’s like `make`, but for building full Linux systems.
- BitBake reads recipes (files ending in `.bb`), which describe:
  - What to build  
  - Where to get the source code  
  - How to compile and install it  
  - What dependencies exist

---

## Build a Small Linux OS Image :

### STEP 1: Install Required Packages

This installs compilers, Python, networking tools, and libraries.

```bash
sudo apt-get update
sudo apt-get install gawk wget git diffstat unzip texinfo
