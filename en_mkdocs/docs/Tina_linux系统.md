# Tina Linux System Introduction
> The D1 Nezha development board comes with the Tina Linux system by default.

Tina Linux is an embedded software system developed by Quanzhi based on the Linux kernel for smart hardware products. openwrt-14.07 is the software development kit for Tina Linux, which contains the kernel source code, drivers, tools, system middleware and application packages for Linux system development.

*openwrt is a well-known open-source embedded Linux system automatic build framework, which is composed of Makefile scripts and Kconfig configuration files. It allows users to compile a complete Linux system software that can be burned directly to the machine through menuconfig configuration.
### System Block Diagram
![](https://d1.docs.allwinnertech.com/assets/img/Tina_Linux_ARCH.png)

The Tina system software architecture is shown in the figure. The four layers are Kernel && Driver, Libraries, System Services, and Applications from the bottom to the top.
#### Kernel && Driver
The Linux Kernel of Tina platform adopts Linux3.4, Linux3.10, Linux4.4, Linux4.9, Linux5.4, etc., and different hardware platforms use different kernel versions to provide security, memory management, process management, network stack, etc. It provides basic support for security, memory management, process management, network stack, etc., and manages device hardware resources such as CPU scheduling, cache, memory, I/O, etc. through the Linux kernel. The D1 is adapted to the Linux 5.4 kernel.

#### Libraries
The libraries layer corresponds to the general embedded system and is equivalent to the middleware level. It contains various system base libraries, third-party open-source library support, and provides API interfaces for the application layer, so that system customizers and application developers can develop new system services and applications based on the APIs in the Libraries layer.

#### System Services
The System Services layer corresponds to the System Services layer, which includes system boot management, configuration management, hot-plugging management, storage management, multimedia middleware, etc.

#### Applications
Applications layer is mainly to implement specific product functions and interaction logic, developers can develop and implement their own applications to provide various system capabilities to end users.

## SDK Structure
Tina Linux SDK mainly consists of build system, configuration tools, toolchain, host toolkit, target device application, documentation, scripts, linux kernel, bootloader parts, the following are the files and directories contained in the main Tina directory.
```
Tina-SDK/
├── build
├── config
├── Config.in
├── device
├── dl
├── lichee
├── Makefile
├── out
├── package
├── prebuilt
├── rules.mk
├── scripts
├── target
├── tmp
├── toolchain
└── tools
```
The following is a brief description of what is contained in the main directories.

### The build directory
The build directory holds the build system files for Tina Linux. The structure of this directory is mainly a series of .mk files based on the Makefile specification, whose main functions are:
（1）Checking whether the current build environment meets the build requirements of Tina Linux.

（2）Generating compilation rules for host packages (PC packages).

（3）Generate the compilation rules for the toolchain.

（4）Generate the compilation rules for the target package.

（5）Generating compilation rules for the linux kernel.

（6）Generate rules for system firmware generation.
```asp
build/
├── autotools.mk
├── aw-upgrade.mk
├── board.mk
├── cmake.mk
├── config.mk
├── debug.mk
├── depends.mk
├── device.mk
├── device_table.txt
├── download.mk
├── dumpvar.mk
├── envsetup.sh
    .....
```

### config directory
The config directory mainly stores the interface of the configuration menu and some fixed configuration items in Tina Linux, which is based on the mconf specification of the kernel.
```
config/
├── Config-build.in
├── Config-devel.in
├── Config-images.in
├── Config-kernel.in
├── Config-systeminit.in
└── top_config.in
```
### device target
The devices directory is used to store configuration files for the solution, including kernel configuration, env configuration, partition table configuration, sys_config.fex (Quanzhi custom board-level configuration file), and board.dts (linux standard device tree file), etc.

*These configurations were stored in the target directory on the old version of Tina (before Tina 3.0), but now they have been moved to the device directory, but defconfig is still stored in the target directory.
```asp
device/
└── config
    ├── chips
    │   └── d1
    └── common
        ├── cert
        ├── debug
        ├── dtb
        ├── hdcp
        ├── imagecfg
        ├── partition
        ├── sign_config
        ├── toc
        ├── tools
        └── version
```
Among them, config/chips/d1 stores D1 platform-related configuration, and its directory structure is as follows.


```asp
d1
├── bin
├── boot-resource
│   └── boot-resource
│       └── bat
├── configs
│   ├── default
│   ├── evb1
│   │   ├── linux -> linux-5.4
│   │   └── linux-5.4
│   └── fpga
│       └── linux-5.4
└── tools
```
- The bin directory holds bin files for compiling boot, etc. When Tina SDK builds or recompiles the boot, the corresponding files will be replaced.
Shortcut jump command: cbin.

- The boot-resource directory stores boot animation and other resources.

- tools directory holds the tools needed to build the solution

- The configs directory holds the configuration files of the hardware solutions for the CHIP platform. The default is the public configuration, evb1 is the configuration of the corresponding hardware evb1 board, and fpga is the configuration of the fpga board. If the same configuration file exists in the public configuration directory default and the solution configuration directory, the solution configuration will be used first.
- Shortcut jump command: cconfigs (this command will jump to the linux directory under this directory).
Take the evb1 scheme as an example, briefly describe the scheme configuration directory with the following details.
```asp
d1/configs/evb1/
├── board.dts -> linux-5.4/board.dts
├── env.cfg
├── linux -> linux-5.4
├── linux-5.4
│   ├── board.dts
│   └── config-5.4
├── sys_config.fex
└── sys_partition.fex
```
board.dts board-level dts configuration file, in line with the linux kernel dts configuration format and merge rules.

env.cfg environment variable configuration file, Uboot will pass this environment variable to the kernel.

linux/config-5.4 Linux5.4 kernel configuration file, configures the default linux kernel functions under the scheme.

sys_config.fex The packaging phase updates the bin file headers of boot0, uboot, optee, etc. according to the sys_config configuration, such as updating the dram parameters, uart parameters, etc.

sys_partition.fex Partition configuration file.

### lichee directory
The lichee directory mainly stores bootloader, linux kernel, DSP code, etc. The DSP code and compilation environment are copyrighted by the DSP vendor, Techsonic, and need to be applied for separately. lichee directory has the following structure.
```asp
Tina-SDK
    ├── brandy-2.0
    │   ├── build.sh
    │   ├── tools
    │   └── u-boot-2018
    └── linux-5.4
```
### package directory
The package directory stores the package source code and compilation rules supported by Tina system. The directory is categorized according to the function of the target package, which contains packages for all platforms of Tina system (including Quanzhi R/H/F/V/T series), but not all packages are adapted to D1 program, some packages need to be adapted by developers.
```asp
package/
├── add-rootfs-demo
├── admin
├── allwinner
    ...
├── utils
└── wayland
```
### prebuild directory
The prebuild directory stores the precompiled cross-compilers, and the directory structure is as follows. gcc/riscv is the toolchain directory used to build D1.
```asp
prebuilt/
└── gcc
    └── linux-x86
        ├── host
        └── riscv
            └── toolchain-thead-glibc
```
### scripts directory
The scripts directory is used to store some scripts used on the host side (PC side, same below) or the target side (small machine side, same below).
> ####Generally, scripts that specify the interpreter as #! /bin/bash scripts are host#! /bin/sh scripts are target-side tools.
```
scripts/
├── add_initramfs.sh
├── arm-magic.sh
├── ...
```
### target directory
The target directory is used to store target board related configuration and specifications generated by sdk and toolchain.
```
target/
    ├── allwinner
    ├── Config.in
    ├── imagebuilder
    ├── Makefile
    ├── sdk
    └── toolchain
```
Shortcut jump command: cdevice.

### toolchain directory
The toolchain directory contains cross toolchain build configurations, rules.
```
toolchain/
├── binutils
├── fortify-headers
├── gcc
├── gdb
├── glibc
├── insight
├── kernel-headers
├── musl
└── wrapper
```
### tools directory
The tools directory is used to store the compilation rules for host-side tools.
out directory
The out directory is used to store the temporary files and final image files related to compilation, which are automatically generated after compilation.

```
out/
├── d1-evb1
└── host
```

The host directory is used to store the host-side tools and some development-related files.

The d1-evb1 directory is the corresponding directory for the program. The structure of the program directory is as follows：

```
out/d1-evb1/
├── boot.img
├── compile_dir
├── d1-evb1-boot.img
├── d1-evb1-Image
├── d1-evb1-uImage
├── image
├── md5sums
├── packages
├── rootfs.img
├── sha256sums
├── staging_dir
├── tina_d1-evb1_uart0.img
└── usr.img
```
Where, - tina_d1-evb1_uart0.img is the final firmware package (system image), and the serial information is output through the serial port. If you use pack -d, the generated firmware package is xxx_card0.img, and the serial port information is forwarded to the tf card holder output.

- boot.img is the data that is finally burned to the system boot partition, it may be in boot.img format or uImage format.
- rootfs.img is the data that is finally burned to the system rootfs partition, which is in squashfs format by default.
- d1-evb1-Image is the kernel's Image format image for further uImage generation.
- d1-evb1-uImage is the kernel's uImage format image, which will be copied to boot.img if configured as uImage format.
- d1-evb1-boot.img is the kernel's boot.img format If configured as boot.img, it will be copied as boot.img
- compile_dir is the temporary file directory where sdk compiles host, target and toolchain, and contains the source code of each package.
- staging_dir is the directory where the results of each directory are stored during the sdk compilation process.
- The packages directory holds the final ipk packages.

Shortcut jump command:cout。
