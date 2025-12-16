## What is the Yocto Project?
The Yocto Project is an open-source framework that provides tools and metadata to build highly customized embedded Linux operating systems according to specific hardware and application requirements.

## Is Yocto a Linux distribution? Why or why not?
Yocto is not a Linux distribution; it is a framework used to build customized Linux distributions for embedded devices.

## Why do we use Yocto instead of Ubuntu or Debian?
Ubuntu is a general-purpose Linux distribution that requires large storage and RAM. In embedded devices, we need a small and customized Linux OS with only required drivers and packages, which is why Ubuntu is not suitable.

## What are the main goals of Yocto?
The main goal of the Yocto Project is to build open-source, highly customized Linux operating systems for embedded devices.

## What is Poky?
Poky is the reference build system and reference distribution provided by the Yocto Project to demonstrate how to build custom Linux distributions.

## What is BitBake?
BitBake is a build automation tool that executes tasks defined in recipes and metadata. While it is conceptually similar to Make, BitBake is more powerful and supports dependency resolution, cross-compilation, and entire Linux image generation.

## What is a recipe (.bb file)?
A recipe is a metadata file in Yocto that tells BitBake how to fetch, configure, compile, and install a software package.

## What is a layer in Yocto?
A layer is a collection of recipes, configuration files, and metadata used to organize the Yocto build system.

## What is bblayers.conf?
bblayers.conf lists all the layers included in the Yocto build

## What is local.conf?
local.conf is used to configure build options such as machine type, image features, and parallel build settings.

## What is an image in Yocto?
An image is a complete Linux filesystem built using multiple recipes.

## What is the difference between image and recipe?
A recipe builds a single package, while an image combines many packages to create a full Linux OS.

## What does BitBake do internally?
BitBake parses metadata, resolves dependencies, and executes tasks like fetch, compile, and install.

## What is SRC_URI?
SRC_URI specifies where the source code is fetched from.

## What is DEPENDS?
DEPENDS lists build-time dependencies.

## What is RDEPENDS?
RDEPENDS lists runtime dependencies.

## Difference between DEPENDS and RDEPENDS?
DEPENDS is for build-time dependencies, while RDEPENDS is for runtime dependencies.

## What is a BSP layer?
A BSP layer contains hardware-specific support such as kernel, bootloader, and device tree files.

## What is MACHINE in Yocto?
MACHINE defines the target hardware platform.

## How do you add a package to an image?
By adding it to IMAGE_INSTALL in the image recipe or local.conf.

## What is cross-compilation?
Cross-compilation means building software on one system for execution on another target system.

## What is SSTATE cache?
SSTATE cache stores prebuilt objects to speed up rebuilds.

## What is do_compile?
do_compile is the task that compiles source code.

## What is .bbappend?
A .bbappend file is used to modify or extend an existing recipe without changing the original.
 
## What is root filesystem (rootfs)?
Rootfs is the first filesystem mounted by the Linux kernel at boot time. It includes directories like /bin, /sbin, /lib, /etc, and /usr, which are necessary for system initialization and application execution.

## What does bitbake <image> do?
bitbake <image> builds a complete Linux image by compiling all required recipes and generating the kernel, root filesystem, and bootable images.
