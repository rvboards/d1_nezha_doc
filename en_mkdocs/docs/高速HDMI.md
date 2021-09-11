### Camera HDMI display (High Speed - HDMI)

**<span style="font-size:16px;">Project name：</span>**<span style="font-size:16px;">Camera HDMI display.</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">The video image data captured by the camera is displayed in real time via HDMI.</span>

<span style="font-size:16px;">

The project is basically the same as the above project, the difference is that the high-speed to HDMI adapter board is used. The camera model used in the experiment is MT9V034, which is described in：

[https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html](https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html "https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html")。

The SCCB protocol is described in：[https://www.cnblogs.com/aslmer/p/5965229.html](https://www.cnblogs.com/aslmer/p/5965229.html "https://www.cnblogs.com/aslmer/p/5965229.html")。

The high-speed port to HDMI adapter board is designed as follows：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628056100/74.png)

**<span style="font-size:16px;">Implementation process：</span>**

<span style="font-size:16px;">

1.Connect the HDMI to the adapter board, connect the camera to the development board with a Dupont cable, and make sure the pins are aligned accurately.

2.Open the project and compile for pin assignment, pin assignment is as follows.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628056203/75.png)

<span style="font-size:16px;">

3.After generating the bitstream file in VIVADO, download it to the FPGA through the downloader, and if the development board is connected to the camera and HDMI at this time, you can see the HDMI display showing the video image captured by the camera.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628056282/76.png)


