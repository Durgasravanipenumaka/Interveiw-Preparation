## Yocto :
- Yocto is not an operating system. It is a build system or framework used to create custom Linux distributions for embedded systems (like boards, IoT devices, routers, automotive systems, etc.).
- Yocto helps you build your own version of Linux — specifically designed for your embedded hardware.

## What Yocto Actually Does
- Yocto automates building all parts of an embedded Linux system:
| Component                    | Yocto Role                                       |
| ---------------------------- | ------------------------------------------------ |
| **Bootloader**               | Builds U-Boot or other loaders                   |
| **Linux Kernel**             | Builds custom kernel with selected configuration |
| **Root Filesystem**          | Builds minimal or full Linux file system         |
| **Applications & Libraries** | Builds your chosen software packages             |
| **Image Generation**         | Produces flashable `.img` or `.tar.gz` files     |

## Yocto is Based On BitBake :
- Yocto’s build engine is called BitBake — it’s like make, but for building full Linux systems.
- BitBake reads recipes (files ending in .bb), which describe:
  What to build
  Where to get the source code
  How to compile and install it
  What dependencies exist

## Build a small Linux OS image :
### STEP 1: Install Required Packages :
This installs compilers, Python, networking tools, and libraries.
```c
sudo apt-get update
sudo apt-get install gawk wget git diffstat unzip texinfo gcc build-essential \
chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils \
iputils-ping libsdl1.2-dev xterm
```
### Download the Yocto Project Source (Poky) :
Poky is the reference build system for Yocto — think of it as the Yocto “core”.
```c
git clone git://git.yoctoproject.org/poky
cd poky
```
### STEP 3: Set Up the Build Environment :
```c
source oe-init-build-env
```
This creates and switches you into a new folder called build/.
Inside it, you’ll find:
```c
build/
 ├── conf/
 │   ├── bblayers.conf
 │   └── local.conf
```
These are the main configuration files:
    - local.conf → your build settings (target machine, image type)
    - bblayers.conf → tells Yocto which layers to use
### STEP 4: Choose a Target Machine :
By default, Yocto builds for QEMU (a virtual machine) — perfect for learning.
```c
MACHINE ?= "qemux86-64"
```
### STEP 5: Build a Minimal Linux Image :
```c
bitbake core-image-minimal
```
### STEP 6: Check Build Output :
When the build finishes, you’ll see:
```c
NOTE: Tasks Summary: 4000 tasks done, 0 failed.
```
Your final image files are stored in:
```c
build/tmp/deploy/images/qemux86-64/
```
### STEP 7: Run the Image in QEMU (Virtual Board) :
```c
runqemu qemux86-64
```
This will open a terminal window with your new Linux OS running — built completely by Yocto!

## What You Just Did ?
| Step | What You Did           | Result                |
| ---- | ---------------------- | --------------------- |
| 1    | Installed dependencies | Environment ready     |
| 2    | Cloned Poky            | Got Yocto source      |
| 3    | Initialized build      | Created `build/conf`  |
| 4    | Chose machine          | Target decided        |
| 5    | Ran BitBake            | Built Linux OS        |
| 6    | Viewed output          | Kernel + RootFS ready |
| 7    | Booted in QEMU         | Tested image          |


