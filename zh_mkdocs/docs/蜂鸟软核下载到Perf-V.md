### 将蜂鸟软核下载到 Perf-V 中

**<span style="font-size:16px;">说明：本例子以 2017.4.1 为例说明使用方法，版本不同但使用方法一样。</span>**

<span style="font-size:16px;">为了方便用户使用，已经将蜂鸟工程文件移植到了 Perf-V 上。</span>

<span style="font-szie:16px;">将公司提供的资料里的蜂鸟的工程文件（在提供资料名称为“蜂鸟工程”文件夹中）</span><span style="font-szie:16px;color:#FF0000;">拷贝到纯英文目录（Vivado 工程不支持中文路径）</span><span style="font-szie:16px;">。</span>

<span style="font-size:16px;">再打开 Vivado 2017.4，如图所示：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372080/17.png)

<span style="font-size:16px;">打开 open Project。找到自己存放蜂鸟工程的位置如图所示：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372137/18.png)

<span style="font-size:16px;">打开工程文件后如图所示：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372184/19.png)

<span style="font-size:16px;">将公司提供的下载器接上 JTAG 口后（注意，不是 USERJTAG）。连接图为：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372403/20.png)

<span style="font-size:16px;">连接好后打开板子电源开关，点击 open Hardware Manager 后如图所示：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372551/22.png)

<span style="font-size:16px;">点击 open target 后再点击 Auto connect 后会自动连接下载器如图所示：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372623/23.png)

<span style="font-size:16px;">再点击 Program device 如图所示：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372697/24.png)

<span style="font-size:16px;">路径中的文件若是工程的 bit 文件路径则点击 program 即可完成下载。若不是，请将路径换成工程的 bit 文件。</span>

<span style="font-size:16px;">到此步骤完成了将蜂鸟工程下载到 Perf-V，但由于 FPGA 掉电后刚刚下载的bit 文件会丢失，所以开发板一旦掉电后，程序也随之消失，还需要再次下载，为了方便可以继续进行一下步骤，将蜂鸟文件固化到 flash 中，掉电也不会丢失。接下来是将蜂鸟工程固化到 flash 的教程。</span>

<span style="font-size:16px;">打开工程此目录 project\project_1.runs\impl_1 搜索 bit 文件 system.bit 将此文
件复制到 D 盘的根目录中。
先将工程生成的 system.bit（若找不到请再工程文件里搜索文件名称）拷贝到D盘根目录中。然后复制此命令
	write_cfgmem -format mcs -interface spix4 -size 128 -loadbit "up 0x0 
	D:/system.bit" -force D:/system.mcs
到 Vivado 的命令框中，如图所示：
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372877/25.png)

<span style="font-size:16px;">
然后点击回车，出现如图所示 write_cfgmem completed successfully。则 bit文件生成 mcs 文件成功。若失败则大多为路径错误，请再次核查路径。

接下来右点击上图中的 xc7a35t_0 选择 add configuration memory device 如图
所示：
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627372951/26.png)

<span style="font-size:16px;">

在 search 中输入：n25q64

选择 n25q64-3.3v 如图所示：

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627373017/27.png)

<span style="font-size:16px;">点击 OK，弹出对话框再点 OK 击如图所示：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627373060/28.png)

<span style="font-size:16px;">在 configuration file 中选择在 D 盘根目录中刚刚生成的 mcs 文件。再点击 OK
则将蜂鸟工程固化到 flash 中。掉电不会丢失。</span>




