### Camera VGA display (High speed - VGA)

**<span style="font-size:16px;">Project name：</span>**<span style="font-size:16px;">Camera VGA display.</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">The video image data captured by the camera is displayed in real time via VGA.</span>

<span style="font-size:16px;">
The architecture of camera VGA display and camera HDMI display is basically the same, only the display module is changed. The camera model used in the experiment is MT9V034, which is described in：

[https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html](https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html "https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html")。

The SCCB protocol is described in detail in：[https://www.cnblogs.com/aslmer/p/5965229.html](https://www.cnblogs.com/aslmer/p/5965229.html "https://www.cnblogs.com/aslmer/p/5965229.html")。

VGA interface is the most widely used type of interface on graphics cards, which transmits red, green, blue analog signals and synchronization signals.
  
Perf-V development board can be connected to the high-speed port - VGA adapter board to achieve the output of VGA signal. The camera is controlled by the SCCB bus to complete the corresponding register configuration; after the configuration is completed, the output data of the camera is collected and finally the data is displayed through VGA to realize the function of VGA real-time video display.

The adapter board is designed as follows：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628067634/77.png)

**<span style="font-size:16px;">Implementation process：</span>**

<span style="font-size:16px;">

1.Connect the VGA interface to the adapter board, connect the camera and the development board with Dupont cable, connect accurately to ensure pin alignment.

2.Open the project and compile the pin assignment, the pin assignment is as follows.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628067804/78.png)

<span style="font-size:16px;">

3.After generating the bitstream file in VIVADO, download it to the FPGA through the downloader, if the development board is connected to the camera and VGA at this time, you can see the VGA display showing the video image captured by the camera.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628067874/79.png)

