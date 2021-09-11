### Hummingbird-based TFT screen display experiment

**<span style="font-size:16px;">Project name：</span>**<span style="font-size:16px;">Hummingbird-based TFT screen display experiment</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">displaying a specified image on a TFT screen</span>


<span style="font-size:16px;">

TFT screen introduction：

This experiment uses a 3.5-inch TFT-LCD, model QD3503728. QD353728 is a color active-matrix liquid crystal module containing amorphous silicon TFT (thin film transistor). It consists of color TFT-LCD panel, driver IC, FPC and backlight unit, the display area of this module contains 320x480 pixels.

ILI9486

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628046785/66.png)

<span style="font-size:16px;">

- Specific requirements：Display the specified content through Hummingbird TFT screen.

- Experimental process：

1、 Open the configured virtual machine, copy the .c, .h and Makefle files in the TFT folder to the directory in the above experiment: /home/a/desktop/1/sirv-e-sdk/software/demo_gpio

2、 connect the JTAG downloader and the computer, the JTAG downloader and the development board, and plug the screen into the development board, as shown below.


</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628047036/67.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628047103/68.png)

<span style="font-size:16px;">

3、 determine the bottom right corner of the interface inside the virtual machine system, the blue mark in the red box in the figure appears, which indicates that the linix system of the virtual machine and the JTAG downloader are connected together.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628047183/69.png)

<span style="font-size:16px;">

4、 to the development board power, according to the above two experiments to compile and download the program, TFT screen can normally display the test program, the following figure.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628047242/70.png)

