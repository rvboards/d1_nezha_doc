# Tina Linux 系统介绍
> D1 哪吒开发板默认自带Tina Linux系统。

Tina Linux是全志科技基于Linux内核开发的针对智能硬件类产品的嵌入式软件系统。Tina Linux基于openwrt-14.07 版本的软件开发包，包含了 Linux 系统开发用到的内核源码、驱动、工具、系统中间件与应用程序包。

*openwrt 是知名的开源嵌入式 Linux 系统自动构建框架，是由 Makefile 脚本和 Kconfig 配置文件构成的。使得用户可以通过 menuconfig配置，编译出一个完整的可以直接烧写到机器上运行的 Linux 系统软件。
### 系统框图
![](https://d1.docs.allwinnertech.com/assets/img/Tina_Linux_ARCH.png)

Tina系统软件架构如图所示。从下至上分别为Kernel && Driver、Libraries、System Services、Applications 四层。
#### Kernel && Driver
Kernel&&Driver 层主要提供 Linux Kernel 的标准实现。Tina 平台的 Linux Kernel 采用 Linux3.4、Linux3.10、Linux4.4、Linux4.9、Linux5.4 等内核，不同硬件平台使用不同内核版本，提供安全性、内存管理、进程管理、网络协议栈等基础支持，并通过 Linux 内核管理设备硬件资源，如 CPU 调度、缓存、内存、I/O 等。 其中D1适配的是Linux 5.4内核。

#### Libraries
Libraries 层对应一般嵌入式系统，相当于中间件层次。其包含了各种系统基础库、第三方开源程序库支持，为应用层提供 API 接口，系统定制者和应用开发者可以基于 Libraries 层的API 开发新的系统服务和应用程序。

#### System Services
System Services 层对应系统服务层，包含系统启动管理、配置管理、热插拔管理、存储管理、多媒体中间件等。

#### Applications
Applications 层主要是实现具体的产品功能及交互逻辑，开发者可以开发实现自己的应用程序，提供系统各种能力给到终端用户。

## SDK结构
Tina Linux SDK 主要由构建系统、配置工具、工具链、host 工具包、目标设备应用程序、文档、脚本、linux 内核、bootloader 部分组成，下面是Tina主目录包含的文件和目录。
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
以下将对主要目录中包含的内容进行简单介绍。

### build 目录
build 目录存放 Tina Linux 的构建系统文件，此目录结构下主要是一系列基于 Makefile 规格编写的 .mk 文件，主要的功能有：
（1）检测当前的编译环境是否满足 Tina Linux 的构建需求；

（2）生成 host 包（PC端软件包）编译规则；

（3）生成工具链的编译规则；

（4）生成 target 包的编译规则；

（5）生成 linux kernel 的编译规则；

（6）生成系统固件的生成规则。
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

### config 目录
config 目录主要存放 Tina Linux 中配置菜单的界面以及一些固定的配置项，该配置菜单基于内核的 mconf 规格编写。
```
config/
├── Config-build.in
├── Config-devel.in
├── Config-images.in
├── Config-kernel.in
├── Config-systeminit.in
└── top_config.in
```
### device 目标
devices 目录用于存放方案的配置文件，包括内核配置、env 配置、分区表配置、sys_config.fex（全志定制板级配置文件）、

board.dts（linux标准设备树文件） 等。

*这些配置在旧版本Tina（Tina3.0以前）上是保存于 target 目录下，现新版本均移到了 device 目录下，但defconfig仍保存在 target 目录下
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
其中，config/chips/d1 存放D1平台相关的配置，其目录结构如下：


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
- bin 目录存放编译 boot 等bin文件，当Tina SDK构建或重新编译boot时，对应的文件会被替换。
快捷跳转命令： cbin。

- boot-resource 目录存放开机动画等资源。

- tools 目录存放方案构建时需要的工具

- configs 目录存放该CHIP平台对应的 多个硬件方案配置文件。其中，default 为公共配置，evb1 对应硬件evb1板的方案配置，fpga 为 fpga板的方案配置，若存在更多个硬件方案，便会在该目录下新建对应的方案目录。 若公共配置目录default和方案配置目录中，存在相同的配置文件时，优先使用方案配置。
- 快捷跳转命令：cconfigs（该命令会跳转到该目录下linux目录）。
以evb1方案为例，简述方案配置目录下，具体内容：
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
board.dts 板级dts配置文件，符合linux内核dts配置格式及合并规则。

env.cfg 环境变量配置文件，Uboot将此环境变量传递给内核。

linux/config-5.4 Linux5.4 内核配置文件，配置方案下默认linux内核功能。

sys_config.fex 打包阶段根据sys_config配置更新boot0, uboot, optee等bin文件的头部等信息，例如更新dram参数、uart参数等。

sys_partition.fex 分区配置文件。
### lichee 目录
lichee 目录主要存放 bootloader、linux内核、DSP等代码，其中DSP代码及编译环境因涉及DSP供应商科声讯版权，需单独申请。lichee目录下结构如下：
```asp
Tina-SDK
    ├── brandy-2.0
    │   ├── build.sh
    │   ├── tools
    │   └── u-boot-2018
    └── linux-5.4
```
### package 目录
package 目录存放Tina系统支持的软件包源码和编译规则，目录按照目标软件包的功能进行分类，该目录包含了Tina系统全平台（包括全志R/H/F/V/T系列）的软件包，但是并不是所有软件包都适配了D1方案，部分软件包需要开发者自行适配。
```asp
package/
├── add-rootfs-demo
├── admin
├── allwinner
    ...
├── utils
└── wayland
```
### prebuild 目录
prebuild目录存放预编译交叉编译器，目录结构如下。 gcc/riscv 即为编译 D1 所用的工具链目录
```asp
prebuilt/
└── gcc
    └── linux-x86
        ├── host
        └── riscv
            └── toolchain-thead-glibc
```
### scripts 目录
scripts目录用于存放host端(PC端，下同)或target端（小机端，即目标机器，下同）使用的一些脚本。
> ####一般指定解释器为#!/bin/bash的脚本是host#!/bin/sh的脚本是target端工具。
```
scripts/
├── add_initramfs.sh
├── arm-magic.sh
├── ...
```
### target 目录
target目录用于存放目标板相关的配置以及sdk和toolchain生成的规格。
```
target/
    ├── allwinner
    ├── Config.in
    ├── imagebuilder
    ├── Makefile
    ├── sdk
    └── toolchain
```
快捷跳转命令：cdevice。

### toolchain 目录
toolchain目录包含交叉工具链构建配置、规则。
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
### tools 目录
tools 目录用于存放 host 端工具的编译规则。
out 目录
out目录用于保存编译相关的临时文件和最终镜像文件 ，编译后自动生成此目录，以编译d1-evb1方案为例说明。

```
out/
├── d1-evb1
└── host
```
其中，host目录用于存放host端的工具以及一些开发相关的文件。

d1-evb1 目录为方案对应的目录。方案目录下的结构如下：

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
其中， - tina_d1-evb1_uart0.img为最终固件包(系统镜像)，串口信息通过串口输出。若使用pack -d，则生成的固件包为xxx_card0.img，串口信息转递到tf卡座输出。
- boot.img为最终烧写到系统boot分区的数据，可能为boot.img格式也可能为uImage格式。
- rootfs.img为最终烧写到系统rootfs分区的数据，该分区默认为squashfs格式。
- d1-evb1-Image 为内核的 Image格式镜像，用于进一步生成uImage。
- d1-evb1-uImage为内核的uImage格式镜像，若配置为uImage格式，则会拷贝成boot.img。
- d1-evb1-boot.img为内核的boot.img格式镜像，若配置为boot.img格式，则会拷贝成boot.img
- compile_dir为sdk编译host，target和toolchain的临时文件目录，存有各个软件包的源码。
- staging_dir为sdk编译过程中保存各个目录结果的目录。
- packages目录保存的是最终生成的ipk软件包。

快捷跳转命令：cout。
