### 摄像头 HDMI 显示(高速--HDMI)

**<span style="font-size:16px;">项目名称：</span>**<span style="font-size:16px;">摄像头 HDMI 显示。</span>

**<span style="font-size:16px;">具体要求：</span>**<span style="font-size:16px;">摄像头采集的视频图像数据通过 HDMI 实时显示。</span>

<span style="font-size:16px;">

该项目和上述项目基本一致，区别在于采用了高速转 HDMI 的转接板。实验中使用的摄像头型号为 MT9V034,具体介绍见：

[https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html](https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html "https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html")。

SCCB 协议具体介绍见：[https://www.cnblogs.com/aslmer/p/5965229.html](https://www.cnblogs.com/aslmer/p/5965229.html "https://www.cnblogs.com/aslmer/p/5965229.html")。

高速口转 HDMI 转接板设计如下：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628056100/74.png)

**<span style="font-size:16px;">实现过程：</span>**

<span style="font-size:16px;">

1.将 HDMI 接到转接板，用杜邦线连接摄像头和开发板，连接准确保证引脚对齐。

2.打开工程编译后进行引脚分配，引脚分配如下：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628056203/75.png)

<span style="font-size:16px;">

3.在 VIVADO 中生成比特流文件后，通过下载器下载到 FPGA 中，如果此时开发板已经连接摄像头和 HDMI 的话，可以看到 HDMI 显示器显示摄像头采集的视频图像。

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628056282/76.png)


