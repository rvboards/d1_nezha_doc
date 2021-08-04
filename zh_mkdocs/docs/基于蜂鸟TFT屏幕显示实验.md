### 基于蜂鸟 TFT 屏幕显示实验

**<span style="font-size:16px;">项目名称：</span>**<span style="font-size:16px;">基于蜂鸟 TFT 屏幕显示实验</span>

**<span style="font-size:16px;">具体要求：</span>**<span style="font-size:16px;">在 TFT 屏幕上显示规定图像</span>


<span style="font-size:16px;">

TFT 屏幕介绍：

本实验采用的是 3.5 寸的 TFT-LCD，型号为 QD3503728。QD353728 是一种含有非晶硅 TFT(薄膜晶体管)的彩色有源矩阵液晶模块。它由彩色 TFT-LCD 面板、驱动 IC、FPC 和背光单元组成，该模块显示区域包含 320x480 像素，本产品符合 RoHS 环保标准，驱动芯片为

ILI9486

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628046785/66.png)

<span style="font-size:16px;">

- 具体要求：通过蜂鸟 TFT 屏幕显示指定内容。

- 实验过程：

1、 打开配置好的虚拟机，将 TFT 文件夹中的*.c、*.h 以及 Makefle 文件复制到上面实验中的目录下： /home/a/desktop/1/sirv-e-sdk/software/demo_gpio

2、 连接好 JTAG 下载器和电脑，JTAG 下载器和开发板，将屏幕插在开发板上，如下图；


</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628047036/67.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628047103/68.png)

<span style="font-size:16px;">

3、 确定虚拟机系统里面界面的右下角，出现图中的红框内的蓝色标记，这表明虚拟机的 linix 系统和 JTAG 下载器连接在一起；

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628047183/69.png)

<span style="font-size:16px;">

4、 给开发板上电，按照上面两个实验的方法编译和下载程序，TFT 屏幕就可以正常显示测试程序，如下图。

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628047242/70.png)

