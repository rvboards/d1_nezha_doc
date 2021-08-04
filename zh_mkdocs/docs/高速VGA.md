### 摄像头 VGA 显示(高速--VGA)

**<span style="font-size:16px;">项目名称：</span>**<span style="font-size:16px;">摄像头 VGA 显示。</span>

**<span style="font-size:16px;">具体要求：</span>**<span style="font-size:16px;">摄像头采集的视频图像数据通过 VGA 实时显示。</span>

<span style="font-size:16px;">
摄像头 VGA 显示和摄像头 HDMI 显示的架构基本一致，只是改变了显示模块。实验中使用的摄像头型号为 MT9V034,具体介绍见：

[https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html](https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html "https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html")。

SCCB 协议具体介绍见：[https://www.cnblogs.com/aslmer/p/5965229.html](https://www.cnblogs.com/aslmer/p/5965229.html "https://www.cnblogs.com/aslmer/p/5965229.html")。

VGA 接口即电脑采用 VGA 标准输出数据接口，是显卡上应用最为广泛的接口类型，它传输红、绿、蓝模拟信号以及同步信号。

Perf-V 开发板可以连接高速口——VGA 的转接板，实现 VGA 信号的输出。摄像头通过 SCCB 总线控制，完成相应的寄存器配置；配置完成后采集摄像头的输出数据，最后将数据通过 VGA 显示，实现 VGA 实时显示视频的功能。

该转接板设计如下：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628067634/77.png)

**<span style="font-size:16px;">实现过程：</span>**

<span style="font-size:16px;">

1.将 VGA 接口接到转接板，用杜邦线连接摄像头和开发板，连接准确保证引脚对齐。

2.打开工程编译后进行引脚分配，引脚分配如下：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628067804/78.png)

<span style="font-size:16px;">

3.在 VIVADO 中生成比特流文件后，通过下载器下载到 FPGA 中，如果此时开发板已经连接摄像头和 VGA 的话，可以看到 VGA 显示器显示摄像头采集的视频图像。

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628067874/79.png)

