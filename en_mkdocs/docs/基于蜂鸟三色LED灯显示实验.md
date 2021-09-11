### Hummingbird-based three-color LED light display experiment

**<span style="font-size:16px;">Project name：</span>**<span style="font-size:16px;">Hummingbird based three-color LED light display experiment</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">to achieve three-color LED flashing by Hummingbird.</span>



**<span style="font-size:16px;">Implementation process：</span>**

<span style="font-size:16px;">

Burn Hummingbird IP core to fpga.

Put the fpga project file into a non-Chinese directory.

1、Connect: jtag port to xilinx jtag.

2、download the ip core of Hummingbird e200 to the development board. As shown in the figure.


</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628038372/29.png)

<span style="font-size:16px;">

Compile and download the c program.

Select demo

Open the configured virtual machine, and open the directory

/home/a/desktop/1/sirv-e-sdk/software/demo_gpio

Copy demo_gpio.from the file "three color led blinking" to the above directory. As shown in the figure below

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628038585/30.png)

<span style="font-size:16px;">

Compile and download the demo

Connect userjtag to the virtual machine

As shown in the figure：/home/a/desktop/1/sirv-e-sdk/bsp/env/sirv-e203-arty

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628038710/31.png)

<span style="font-size:16px;">

Open the directory /home/a/desktop/1/sirv-e-sdk

Compile the target file: open a terminal in the directory and type make upload PROGRAM=demo_gpio BOARD=sirv-e203-arty

As shown in the figure：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628038927/32.png)

<span style="font-size:16px;">

Download target file: input in the terminal make upload PROGRAM=demo_gpio BOARD=sirv-e203-arty

As shown in the figure：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039026/33.png)

<span style="font-size:16px;">

If the following message appears during the process, the download is successful:

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039085/34.png)

<span style="font-size:16px;">

If there is an error in the download and the device is not found, as shown in the figure.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039293/35.png)

<span style="font-size:16px;">

then it may be that the device name needs to be changed. Open the directory

/home/a/desktop/1/sirv-e-sdk/bsp/env/sirv-e203-arty

and open the file shown below.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039373/36.png)

<span style="font-size:16px;">Open the file and change the information in the diagram to the appropriate device name.</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628039940/37.png)

