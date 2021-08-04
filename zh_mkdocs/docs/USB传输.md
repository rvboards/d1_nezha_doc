### USB 传输

**<span style="font-size:16px;">项目名称：</span>**<span style="font-size:16px;">USB 传输。</span>

**<span style="font-size:16px;">具体要求：</span>**<span style="font-size:16px;">基于 PERF-V 开发板完成 USB 数据传输。</span>

<span style="font-size:16px;">
在设计中使用了高速口转 2.54 接口的转接板，详细设计如下：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069608/90.png)

**<span style="font-size:16px;">实现过程：</span>**

<span style="font-size:16px;">
1 安装 USB2.0 模块开发软件：开发本 USB2.0 模块，需要用到两个软件，分别为 CySuiteUSB_3_4_5_B192.exe和 ez_usb_fx2lp_development_kit.exe”，只需要双击安装包，并一路选择 Next即可完成安装。

2 安装本 USB2.0 模块的标准驱动程序：本模块在要能够让电脑识别并正常读写数据之前，需要安装驱动程序。由于目前大部分用户电脑为 win7 或者更高版本的系统，而 win7 及以上版本安装本模块是需要验证驱动签名。官方提供的驱动是没有经过驱动签名验证的，因此我们需要关闭掉系统的驱动签名。
使用 USB 线连接 USB 模块和电脑的 USB 接口，此时，系统右下角应该会弹 出发现新硬件，并且驱动安装失败。

查看设备管理器中，应该能看到如下所示的一个未知设备，我们选中该设备，点击鼠标右键，即可查看其详细信息。在详细信息这一栏我，我们在属性的下拉表中选择“硬件 ID”，可以看到，其值为 USB\VID_040B&PID_8613，这就是我们的 USB2.0 模块的硬件 ID。

切换到驱动程序选项卡，选择“更新驱动程序‘，如下图所示：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069776/91.png)

<span style="font-size:16px;">
在弹出的界面中，选择”浏览计算机以查找驱动程序软件“，路径定位到我们提供的 USB 开发包的驱动程序安装路径下，然后点击确定。

接着点击下一步，会弹出如下所示的界面，点击始终安装：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069847/92.png)

<span style="font-size:16px;">
接着我们回到设备管理器中，在通用串行总线控制器下，可以看到如下所示的设备，且无叹号提示异常，则表明驱动程序安装正确。

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069902/93.png)

<span style="font-size:16px;">
3 烧写 USB2.0 芯片固件

接着我们打开 CyConsole EZ-USB 软件，来烧写我们用于测试的 USB 块传输固件。软件打开后，在 Device 一栏可以看到我们的 Cypress USB XXX 设备，如下图所示：
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069974/94.png)

<span style="font-size:16px;">
接着我们点击 Lg EEPROM 按钮，会打开文件选择框，然后定位到我们提供 USB 芯片固件位置，选中 bulkloop.iic 文件，双击该文件即可打开并自动开始固件下载。

固件下载完成后拔掉 USB 电缆重新连接，然后在界面的 Device 窗口中可以看到设备名变为了 REIMU，接着我们切换到 Cypress USB Console 软件，可以看到已经发现了设备。
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628070045/95.png)

<span style="font-size:16px;">
4 FPGA 写 USB 测试

将 FPGA 程序下载到开发板，回到 Cypress USB Console 工具中来，切换到 Other Endpt Xfers 选项，然后选择 0x86(in)，修改 Bytes of Data 为 1024，然后点击 Transfer Data 按钮，接着就能在 Console 中看到接收到的数据，与实际发送的数据进行核对。
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628070119/96.png)

<span style="font-size:16px;">
数据的组织方式为连续两个 8 位的数据组成一个 16 位的数据。例如接收到数据的最后一行，01 F9 组合在一起，实际值就是 505，最后的 02 00 组合在一起就是 512.。因为我们的测试工程中就是连续从 1 发到 512，因此可知数据传输正确。
</span>


