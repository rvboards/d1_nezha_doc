### Hummingbird based LED dot matrix experiment

**<span style="font-size:16px;">Project name：</span>**<span style="font-size:16px;">Hummingbird-based LED dot matrix experiment</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">to achieve the LED dot matrix cycle through Hummingbird to display the name of this development board.</span>



**<span style="font-size:16px;">Introduction of the LED dot matrix:</span>**

<span style="font-size:16px;">

LED dot matrix screen is composed of LED (light emitting diode), the light beads light up and down to display text, pictures, animation, video, etc., is modular display components, usually by the display module, control system and power supply system. LED dot matrix display is simple to produce, easy to install, is widely used in various public places, such as car annunciators, advertising screens and bulletin boards, etc.

Take a simple 8X8 dot matrix for example, it consists of 64 light-emitting diodes, and each light-emitting diode is placed on the intersection of the line and column lines, when the corresponding line set 1 level, a column set 0 level, the corresponding diode will light; such as the first point to light up, then the 9 pin to high level 13 pin to low level, then the first point will light up; if the first line to light up, then the 9 pin to connect high, and (13, 3, 4, 10, 6, 11, 15, 16) these pins to low, then the first line will be lit; such as to light the first column, then the 13 pin to low, and (9, 14, 8, 12, 1, 7, 2, 5) to high, then the first column will be lit.

</span>

**<span style="font-size:16px;">Experimental procedure：</span>**

<span style="font-size:16px;">

Burn the Hummingbird IP core into the fpga.

Put the fpga project file into a non-Chinese directory.

1、Connect: jtag port to xilinx jtag. user jtag port to connect.

3、Download the ip core of Hummingbird e200 to the development board.
  
As shown in the figure.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628040303/38.png)

<span style="font-size:16px;">

Compile and download the c program.

Select demo

Open the configured virtual machine, and open the directory

/home/a/desktop/1/sirv-e-sdk/software/demo_gpio

Copy demo_gpio. from the file "led dot matrix cyclic display board name" to the above directory.

As shown in the figure below

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628040482/39.png)

<span style="font-size:16px;">

Compile and download the demo

Connect userjtag to the virtual machine

As shown in the figure：/home/a/desktop/1/sirv-e-sdk/bsp/env/sirv-e203-arty

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628040567/40.png)

<span style="font-size:16px;">

Open the directory /home/a/desktop/1/sirv-e-sdk

Compile the target file: open a terminal in the directory and type  make upload PROGRAM=demo_gpio BOARD=sirv-e203-arty

As shown in the figure.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628040689/41.png)

<span style="font-size:16px;">

Download the target file: Open a terminal and type  make upload PROGRAM=demo_gpio BOARD=sirv-e203-arty

As shown in the figure.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041113/42.png)

<span style="font-size:16px;">If the following message appears during the process, the download is successful:</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041215/43.png)

<span style="font-size:16px;">If there is an error in the download and the device is not found, as shown in the figure.</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041275/44.png)

<span style="font-size:16px;">

then it may be that the device name needs to be changed. Open the directory
  
/home/a/desktop/1/sirv-e-sdk/bsp/env/sirv-e203-arty

and open the file shown in the following figure.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041376/45.png)

<span style="font-size:16px;">

Open the file and change the information in the figure to the corresponding device name.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041470/46.png)

<span style="font-size:16px;">

The display effect is PERF-V The cyclic display part of the picture is as follows.
  
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041649/47.png)

<span style="font-size:16px;">

The 8*8 dot matrix schematic diagram is as follows

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041816/48.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041865/49.png)

<span style="font-size:16px;">The wiring of the board is as follows</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041959/50.png)

<span style="font-size:16px;">If you want to modify the display content, use the mold taking software and put the mold taking data into the table array of the program, as shown in the figure:</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628042023/51.png)

