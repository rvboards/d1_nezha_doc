### 基于蜂鸟三色 LED 灯显示实验

**<span style="font-size:16px;">项目名称：</span>**<span style="font-size:16px;">基于蜂鸟三色 LED 灯显示实验</span>

**<span style="font-size:16px;">具体要求：</span>**<span style="font-size:16px;">通过蜂鸟实现三色 LED 变化闪烁。</span>



**<span style="font-size:16px;">实现过程：</span>**

<span style="font-size:16px;">

烧录蜂鸟 IP 核到 fpga 中。

将 fpga 工程文件放到非中文目录中。

1、连线：jtag 口连接 xilinx jtag。User jtag 口连接。

2、下载蜂鸟 e200 的 ip 核到开发板中。如图所示：


</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628038372/29.png)

<span style="font-size:16px;">

编译并下载 c 程序。

选择 demo

打开配置好的虚拟机，并打开目录

/home/a/desktop/1/sirv-e-sdk/software/demo_gpio

将文件“三色 led 闪烁”中的 demo_gpio.复制到上述目录中。如下图所示

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628038585/30.png)

<span style="font-size:16px;">

编译下载 demo

将 userjtag 连接虚拟机

如图所示：/home/a/desktop/1/sirv-e-sdk/bsp/env/sirv-e203-arty

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628038710/31.png)

<span style="font-size:16px;">

打开目录/home/a/desktop/1/sirv-e-sdk

编译目标文件：在目录中打开终端输入 make upload PROGRAM=demo_gpio BOARD=sirv-e203-arty

如图所示：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628038927/32.png)

<span style="font-size:16px;">

下载目标文件：在终端中输入 make upload PROGRAM=demo_gpio BOARD=sirv-e203-arty

如图所示：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039026/33.png)

<span style="font-size:16px;">

过程中出现下图信息则表明下载成功:

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039085/34.png)

<span style="font-size:16px;">

若下载中出现错误，未发现设备，如图所示：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039293/35.png)

<span style="font-size:16px;">

则可能为需要修改设备名称。打开目录

/home/a/desktop/1/sirv-e-sdk/bsp/env/sirv-e203-arty

并打开下图所示文件：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039373/36.png)

<span style="font-size:16px;">打开文件将图中的信息改成相应设备名称：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039940/37.png)

