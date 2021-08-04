### 基于蜂鸟 LED 点阵实验

**<span style="font-size:16px;">项目名称：</span>**<span style="font-size:16px;">基于蜂鸟 LED 点阵实验</span>

**<span style="font-size:16px;">具体要求：</span>**<span style="font-size:16px;">通过蜂鸟实现 LED 点阵循环显示本开发板的名称。</span>



**<span style="font-size:16px;">LED 点阵简介：</span>**

<span style="font-size:16px;">

LED 点阵屏通过 LED(发光二极管）组成，以灯珠亮灭来显示文字、图片、动画、视频等，是各部分组件都模块化的显示器件，通常由显示模块、控制系统及电源系统组成。LED 点阵显示屏制作简单，安装方便，被广泛应用于各种公共场合，如汽车报站器、广告屏以及公告牌等

以简单的 8X8 点阵为例，它共由 64 个发光二极管组成，且每个发光二极管是放置在行线和列线的交叉点上，当对应的某一行置 1 电平，某一列置 0 电平，则相应的二极管就亮；如要将第一个点点亮，则 9 脚接高电平 13 脚接低电平，则第一个点就亮了；如果要将第一行点亮，则第 9 脚要接高电平，而（13、3、4、10、6、11、15、16）这些引脚接低电平，那么第一行就会点亮；如要将第一列点亮，则第 13 脚接低电平，而（9、14、8、12、1、7、2、5）接高电平，那么第一列就会点亮.

</span>

**<span style="font-size:16px;">实验过程：</span>**

<span style="font-size:16px;">

烧录蜂鸟 IP 核到 fpga 中。

将 fpga 工程文件放到非中文目录中。

1、连线：jtag 口连接 xilinx jtag。User jtag 口连接。

3、下载蜂鸟 e200 的 ip 核到开发板中。如图所示：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628040303/38.png)

<span style="font-size:16px;">

编译并下载 c 程序。

选择 demo

打开配置好的虚拟机，并打开目录

/home/a/desktop/1/sirv-e-sdk/software/demo_gpio

将文件“led 点阵循环显示板子名称”中的 demo_gpio.复制到上述目录中。

如下图所示

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628040482/39.png)

<span style="font-size:16px;">

编译下载 demo

将 userjtag 连接虚拟机

如图所示：/home/a/desktop/1/sirv-e-sdk/bsp/env/sirv-e203-arty

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628040567/40.png)

<span style="font-size:16px;">

打开目录/home/a/desktop/1/sirv-e-sdk

编译目标文件：在目 录中打开终端输入 make upload PROGRAM=demo_gpio BOARD=sirv-e203-arty

如图所示：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628040689/41.png)

<span style="font-size:16px;">

下载目标文件：在终端中输入 make upload PROGRAM=demo_gpio BOARD=sirv-e203-arty

如图所示：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041113/42.png)

<span style="font-size:16px;">过程中出现下图信息则表明下载成功:</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041215/43.png)

<span style="font-size:16px;">若下载中出现错误，未发现设备，如图所示：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041275/44.png)

<span style="font-size:16px;">

则可能为需要修改设备名称。打开目录

/home/a/desktop/1/sirv-e-sdk/bsp/env/sirv-e203-arty

并打开下图所示文件：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041376/45.png)

<span style="font-size:16px;">

打开文件将图中的信息改成相应设备名称：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041470/46.png)

<span style="font-size:16px;">

显示效果为 PERF-V 循环显示部分图片如下：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041649/47.png)

<span style="font-size:16px;">

8*8 点阵原理图为：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041816/48.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041865/49.png)

<span style="font-size:16px;">板子的接线为：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628041959/50.png)

<span style="font-size:16px;">若修改显示内容则使用取模软件，将取模数据放入程序的 table 数组中，如图所示:</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628042023/51.png)

