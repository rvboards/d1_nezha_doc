### Camera HDMI Display (High Speed - HDMI & Camera)

**<span style="font-size:16px;">Project name：</span>**<span style="font-size:16px;">Camera HDMI display.</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">Video image data captured by the camera is displayed in real time via HDMI.</span>

**<span style="font-size:16px;">System design：</span>**

<span style="font-size:16px;">

Perf-V development board can be connected to the high-speed port - HDMI & camera adapter board to realize the display of video images. The camera is controlled by SCCB bus to complete the corresponding register configuration; after the configuration is completed, the output data of the camera is collected and finally the data is displayed through HDMI to complete the function of HDMI real-time video display.
  
HDMI is a high-definition multimedia interface, a digital video/audio interface technology, suitable for video transmission of a dedicated digital interface, which can transmit both audio and video signals.

The camera model used in the experiment is MT9V034, which is described in：

[https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html](https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html "https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html")

SCCB protocol is described in：[https://www.cnblogs.com/aslmer/p/5965229.html](https://www.cnblogs.com/aslmer/p/5965229.html "https://www.cnblogs.com/aslmer/p/5965229.html")。

High-speed port to HDMI & camera adapter board is designed as follows：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628054934/71.png)

**<span style="font-size:16px;">Experimental process：</span>**

<span style="font-size:16px;">
1.Connect the camera and HDMI to the adapter board to ensure accurate pin alignment.

2.Compile the program and make the pin assignment, after connecting the adapter board, the pin assignment is as follows.
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628055468/72.png)

<span style="font-size:16px;">
3.Generate the bitstream file in VIVADO and download it to the FPGA via the downloader, if the development board is connected to the camera and HDMI, you can see the HDMI display showing the video image captured by the camera. （</span><span style="font-size:16px;color:#FF0000;">Note: The focal length of the camera module is adjustable, if the focal length is not suitable, the image will be blurred, rotate the lens to adjust the focal length. The camera module should be handled gently, do not touch the components with your hands.</span><span style="font-size:16px;">）
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628055589/73.png)

