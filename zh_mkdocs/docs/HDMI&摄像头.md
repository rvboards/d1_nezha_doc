### 摄像头 HDMI 显示(高速--HDMI&摄像头)

**<span style="font-size:16px;">项目名称：</span>**<span style="font-size:16px;">摄像头 HDMI 显示。</span>

**<span style="font-size:16px;">具体要求：</span>**<span style="font-size:16px;">摄像头采集的视频图像数据通过 HDMI 实时显示。</span>

**<span style="font-size:16px;">系统设计：</span>**

<span style="font-size:16px;">

Perf-V 开发板可以连接高速口——HDMI&摄像头的转接板，实现视频图像的显示。摄像头通过 SCCB 总线控制，完成相应的寄存器配置；配置完成后采集摄像头的输出数据，最后将数据通过 HDMI 显示，完成 HDMI 实时显示视频的功能。

HDMI 是高清晰度多媒体接口，是一种数字化视频/音频接口技术，适合影像传输的专用型数字化接口，可同时传送音频和影像信号。

实验中使用的摄像头型号为 MT9V034,具体介绍见：

[https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html](https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html "https://wenku.baidu.com/view/469a7291daef5ef7ba0d3c6e.html")

SCCB 协议具体介绍见：[https://www.cnblogs.com/aslmer/p/5965229.html](https://www.cnblogs.com/aslmer/p/5965229.html "https://www.cnblogs.com/aslmer/p/5965229.html")。

高速口转 HDMI&摄像头的转接板设计如下：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628054934/71.png)

**<span style="font-size:16px;">实验过程：</span>**

<span style="font-size:16px;">
1.将摄像头和 HDMI 接到转接板连接准确保证引脚对齐。

2.编译程序并进行引脚分配，连接该转接板后引脚分配如下：
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628055468/72.png)

<span style="font-size:16px;">
3.在 VIVADO 中生成比特流文件后，通过下载器下载到 FPGA 中，如果此时开发板已经连接摄像头和 HDMI 的话，可以看到 HDMI 显示器显示摄像头采集的视频图像。（</span><span style="font-size:16px;color:#FF0000;">注意： 摄像头模块焦距是可调的，如果焦距不合适，图像会模糊，旋转镜头可以调节焦距。摄像头模块要轻拿轻放，不要用手触摸元器件。</span><span style="font-size:16px;">）
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628055589/73.png)

