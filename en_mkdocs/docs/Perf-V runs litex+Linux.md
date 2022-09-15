# Operating environment
1、The **Litex** environment runs on `Ubuntu 20.04 LTS`

2、**Vivado** is version 2019.2, running on `windows 10`

Notes：

1. **Litex** can also run on `WSL2`, not expanded here.

2. **Vivado** can also run in a Linux environment, so I won't expand it here.

# Litex running steps

## I. Litex environment installation (Linux)

1. First clone **Litex** to the local
```sh
git https://github.com/enjoy-digital/litex.git
```
2. Follow the steps in [README.md](https://github.com/enjoy-digital/litex/blob/master/README.md) in the **Litex** library to configure the basic operating environment of Litex. Two additional amendments:

(1) In **step 2** of README.md, merge the `--update` parameter into the previous step, that is, execute:
```sh
$ ./litex_setup.py --init --install --update --user (--user to install to user directory) --config=(minimal, standard, full)
```
Otherwise, there will be some problems in the subsequent environment.

(2) After **step 3** of README.md, you need to manually import the riscv-gcc tool path downloaded by it into the environment variable, that is:
```sh
$ export PATH=$PATH:$PWD/riscv64-unknown-elf-gcc-8.1.0-2019.01.0-x86_64-linux-ubuntu14/bin/
```
It is recommended to write this statement into `"~/.bashrc"`, which is convenient for subsequent use.

## II. Code import of Perf V1 (Linux)

1. In Litex, about the generation of `logic code` (Verilog HDL code) and `ROM firmware` (Bootloader and some drivers) of SOC, in [Litex-boards](https://github.com/litex-hub/ litex-boards.git) project. The library is automatically downloaded when the Litex environment is installed. The directory structure of Litex-boards is:

```
litex_boards
    ├── platforms
    ├── prog
    ├── targets
    __init__.py
```
in:

The `platforms` directory defines the board-related IO, clocks, constraints, and some tcl scripts when generating the board's bit stream

The `targets` directory is the code for creating the SOC, in this directory, you can configure the components of the SOC (Ethernet, DRAM, GPIO, etc.)

2. At present, the `platforms` and `targets` codes related to Perf V1 have not been submitted to the author of [enjoy-digital](https://github.com/enjoy-digital), so you need to manually import the relevant codes into the corresponding `platforms' ` and `targets` directories.

Current Pefv V1 code, including **LED marquee**, **button/dip switch**, **UART serial port**, **JTag debug port**, **SPI FLASH**, **DDR3 SDRAM ** and other functions.

TODO: The current Pefv V1 code does not configure **XADC** and **PMOD** related physical information and SOC generation logic.

## III. Litex SOC generation of Perf V1 (Linux + Windows)

1. Generation of SOC `logic code` (Verilog HDL code) and `ROM firmware` (Bootloader and some drivers):
In any `Linux` directory, execute the following statement:
```sh
 python3 -m litex_boards.targets.perf_v1 --cpu-type=naxriscv --no-compile-gateware --build
 ```

The following directory will be generated in the `current directory`:

 ```
build
    ├── gateware
    ├── software
```
In：

`gateware` directory generates `logic code` (Verilog HDL code) and `XDC constraint files`
The `software` directory generates the `ROM firmware` Bootloader and some drivers

2. Personal habit to use `Vivado` under `Windows`, copy the **perf\_v1.v**, **perf\_v1.init**, * generated in the `gateware` directory in **step 1 perf\_v1.xdc** file, copy it to the windows directory, then open **perf\_v1.tcl** in the `gateware` directory with a text editor, put the two files mentioned after the `read\_verilog` command **Ram\_1w\_1rs\_Generic.v** and **NaxRiscvLitex\_e387b4a19000a10fcd6fe95fbfcb8673.v** are copied in together. After selecting the corresponding device, directly import all the above files to create a project and generate a bitstream file.

Note: If the Vivado environment is already installed in the Linux environment, you can directly call perf_v1.sh in the `gateware` directory or directly generate a bitstream.

## IV. Litex running of Perf V1 (Windows)

Download the generated bitstream to the Perf V1 board, open the serial port tool, set **baud rate** to 115200, and you will see the following print:

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1663222314/3.png)

## Perf V1 for Linux (Linux)
1. **Image** + **rootfs.cpio**

Download the script [init.sh](https://github.com/SpinalHDL/NaxSoftware/blob/main/init.sh) under the **NaxSoftWare** project, execute the script, the following directory will be generated:

 ```
images
    ├── rv32ima
    ├── rv32imac
    ├── rv64ima
    ├── rv64imac
    ├── rv64imafdc
```
Copy the **Image** + **rootfs.cpio** files in the `rv32ima` directory.

2.**opensbi**

Download the precompiled linux image file [linux_2022_03_23.zip](https://github.com/litex-hub/linux-on- litex-vexriscv/files/8331338/linux_2022_03_23.zip), decompress and copy the **opensbi.bin** file.

3. **DTB file**

A DTS template is provided here, the file name is **linux.dts**, which can also be manually modified as needed:

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

Compile it into a dtb file using the dtc command:
```
dtc -I dts -O dtb linux.dts -o linux.dtb
```

4. Download Linux to Perf V1

(1) Create a **boot.json** file
```sh
{
    "Image":        "0x40000000",
    "linux.dtb":    "0x40ef0000",
    "rootfs.cpio":  "0x41000000",
    "opensbi.bin":  "0x40f00000"
}
```
Note, if the above 4 files are not in the same directory, please manually modify the relative path

(2) Use the `litex_term` tool to download the image to the Perf V1 board through the `serial port`:

Switch to the same level directory as boot.json, assuming that `UART serial port` is recognized as **ttyUSB0** in Linux,

```sh
$ litex_term --images=boot.json /dev/ttyUSB0
```

At the litex command line interactive prompt that appears, enter:
```sh
$ serialboot
```
Wait for the image loading to complete, limited by the serial port rate, it is expected to be about 20 minutes, and do not perform any operations on the command line during this period.

Then you will see OpenSbi print:

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1663222259/1.png)

Finally, the `"buildroot:"` prompt appears, indicating that the Linux loading is complete:

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1663222298/2.png)

Link：https://pan.baidu.com/s/1mQHqKaCxYuenaWMjSOADJg 
Extraction code：perf
