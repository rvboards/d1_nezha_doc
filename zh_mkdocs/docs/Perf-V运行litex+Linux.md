# 运行环境
1、**Litex**的环境运行在`Ubuntu 20.04 LTS`上

2、**Vivado**的版本为2019.2，运行在`windows 10`上

注：

1、**Litex**也可以运行在`WSL2`上，在此不做展开。

2、**Vivado**也可以运行在Linux环境里，在此不做展开。

# Litex运行步骤

## 一、Litex环境安装（Linux）

1、首先把**Litex**克隆到本地
```sh
git https://github.com/enjoy-digital/litex.git
```
2、按照**Litex**库中[README.md](https://github.com/enjoy-digital/litex/blob/master/README.md)的步骤，将Litex的基本运行环境配置好。补充说明两点修改：

(1) 在README.md的**步骤2**时，把`--update`参数合并到前一步，即执行：
```sh
$ ./litex_setup.py --init --install --update --user (--user to install to user directory) --config=(minimal, standard, full)
```
否则后续环境会出现一些问题。

(2) 在README.md的**步骤3**之后，需要手动把它下载的riscv-gcc工具路径导入到环境变量，即：
```sh
$ export PATH=$PATH:$PWD/riscv64-unknown-elf-gcc-8.1.0-2019.01.0-x86_64-linux-ubuntu14/bin/
```
建议将该语句写入到`"~/.bashrc"`里，方便后续使用。

## 二、Perf V1的代码导入（Linux）

1、Litex中，关于SOC的`逻辑代码`（Verilog HDL代码）和`ROM固件`（Bootloader及一些驱动）的生成，在[Litex-boards](https://github.com/litex-hub/litex-boards.git)工程里。Litex环境安装时，会自动下载该库。Litex-boards的目录结构为：

```
litex_boards
    ├── platforms
    ├── prog
    ├── targets
    __init__.py
```
其中：

`platforms`目录定义了板卡相关的IO、时钟、约束，以及生成板卡bit流时的一些tcl脚本

`targets`目录为创建SOC的代码，可在该目录下，配置SOC的组件（以太网，DRAM，GPIO之类的）

2、目前，Perf V1相关的`platforms`和`targets`代码，未提交给[enjoy-digital](https://github.com/enjoy-digital)作者, 所以需要手动将相关代码导入对应`platforms`和`targets`目录中。

当前Pefv V1代码，包含**LED跑马灯**、**按键/拨码开关**、**UART串口**，**JTag调试口**、**SPI FLASH**，**DDR3 SDRAM**等功能。

TODO: 当前Pefv V1代码，未配置**XADC**和**PMOD**相关的物理信息和SOC生成逻辑。

## 三、Perf V1的Litex SOC生成（Linux + Windows）

1、SOC的`逻辑代码`（Verilog HDL代码）和`ROM固件`（Bootloader及一些驱动）的生成：
在`Linux` 任一目录里，执行下面语句：
```sh
 python3 -m litex_boards.targets.perf_v1 --cpu-type=naxriscv --no-compile-gateware --build
 ```

 会在`当前目录`里生成如下目录：

 ```
build
    ├── gateware
    ├── software
```
其中：

`gateware`目录生成了`逻辑代码`（Verilog HDL代码）和`XDC约束文件`
`software`目录生成了`ROM固件`Bootloader及一些驱动

2、个人习惯在`Windows`下使用`Vivado`，将**步骤1**中`gateware`目录下生成的**perf\_v1.v**、**perf\_v1.init**、**perf\_v1.xdc**文件，拷贝到windows的目录里，然后文本编辑打开`gateware`目录下**perf_v1.tcl**，把`read_verilog`命令后提到的两个文件**Ram\_1w\_1rs\_Generic.v**和**NaxRiscvLitex\_e387b4a19000a10fcd6fe95fbfcb8673.v**一并拷入。选择好对应器件后，直接导入上述所有文件创建工程，生成bitstream文件。

注：如果在Linux环境下，已经装有Vivado环境，可以在`gateware`目录里直接调用perf_v1.sh也可以直接生成bitstream。

## 四、Perf V1的Litex运行（Windows）

将生成的bitstream下载到Perf V1板卡中，打开串口工具，**波特率**设为115200，会看到如下打印：
![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1663222314/3.png)

## Perf V1的Linux运行（Linux）
1、**Image** + **rootfs.cpio**

下载**NaxSoftWare**工程下的该脚本[init.sh](https://github.com/SpinalHDL/NaxSoftware/blob/main/init.sh),执行该脚本，将生成以下目录：

 ```
images
    ├── rv32ima
    ├── rv32imac
    ├── rv64ima
    ├── rv64imac
    ├── rv64imafdc
```
将`rv32ima`目录里的**Image** + **rootfs.cpio**文件拷贝出来.

2、**opensbi**

下载**litex-hub**下**linux-on-litex-vexriscv**库提供的预编译linux镜像文件[linux_2022_03_23.zip](https://github.com/litex-hub/linux-on-litex-vexriscv/files/8331338/linux_2022_03_23.zip),解压后将其中**opensbi.bin**文件拷贝出来。

3、**DTB文件**

此处提供一个DTS的模板，文件名为**linux.dts**，也可以根据需要手动修改：

```sh
/dts-v1/;

/ {
    #address-cells = <0x01>;
    #size-cells = <0x01>;
    compatible = "spinal,naxriscv";
    model = "spinal,naxriscv_sim";

    chosen {
        bootargs = "rootwait console=hvc0 earlycon=sbi root=/dev/ram0 init=/sbin/init";
        linux,initrd-start = <0x41000000>;
        linux,initrd-end = <0x41800000>;
    };

    cpus {
        #address-cells = <0x01>;
         #size-cells = <0x00>;
        timebase-frequency = <0x5f5e100>;

        cpu@0 {
            device_type = "cpu";
            compatible = "riscv";
            riscv,isa = "rv32ima";
            mmu-type = "riscv,sv32";
            reg = <0x00>;
            status = "okay";

            interrupt-controller {
                #interrupt-cells = <0x01>;
                interrupt-controller;
                compatible = "riscv,cpu-intc";
            };
        };
    };

    memory@40000000 {
        device_type = "memory";
        reg = <0x40000000 0x4000000>;
    };
};
```

使用dtc命令将其编译为dtb文件：
```
dtc -I dts -O dtb linux.dts -o linux.dtb
```

4、下载Linux到Perf V1

(1) 建立**boot.json**文件
```sh
{
    "Image":        "0x40000000",
    "linux.dtb":    "0x40ef0000",
    "rootfs.cpio":  "0x41000000",
    "opensbi.bin":  "0x40f00000"
}
```
注，如果上述4个文件不在同一目录，请手动修改相对路径

(2) 使用`litex_term`工具，通过`串口`下载镜像到Perf V1板卡里：
切换到boot.json同级目录，假设`UART串口`在Linux中识别为**ttyUSB0**，

```sh
$ litex_term --images=boot.json /dev/ttyUSB0
```

在出现的`litex`命令行交互提示符后，输入：
```sh
$ serialboot
```
等待镜像加载完成，受限于串口速率，预计20分钟左右，此期间不要在该命令行进行任何操作。
随后会看到OpenSbi的打印:

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1663222259/1.png)

最后出现`"buildroot:"`提示符，说明Linux加载完成：

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1663222298/2.png)

链接：https://pan.baidu.com/s/1mQHqKaCxYuenaWMjSOADJg 

提取码：perf
