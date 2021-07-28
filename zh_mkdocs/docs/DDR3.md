### DDR3

<span style="font-size:16px;">

本开发板板载了一片高速 DDR3 SDRAM， 型号：MT41J128M16JT-093， 容量：256MByte（128M*16bit），16bit 总线。开发板上 FPGA 和 DDR3 SDRAM 相连的是 BANK35 的 IO，DDR3 的硬件设计需要严格考虑信号完整性，我们在电路设计和 PCB 设计的时候已经充分考虑了匹配电阻/终端电阻，走线阻抗控制，走线等长控制，保证 DDR3 高速稳定的工作。

</span>

**<span style="font-size:16px;">项目名称：</span>**<span style="font-size:16px;">DDR3。</span>

**<span style="font-size:16px;">具体要求：</span>**<span style="font-size:16px;">实现 DDR3 数据的读写。</span>

**<span style="font-size:16px;">系统设计：</span>**

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476573/1.png)

**<span style="font-size:16px;">实现过程：</span>**

<span style="font-size:16px;">1.新建工程之后打开 Create Block Design，并修改 Design name。</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476665/2.png)

<span style="font-size:16px;">
2.按照系统设计依次添加 IP 并完成连线。
3.按照下图对 IP 进行相应的配置。
</span>

**<span style="font-size:16px;">Axi Datamover 配置：</span>**

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476756/3.png)

**<span style="font-size:16px;">mig_7_series 配置：</span>**

<span style="font-size:16px;">打开该 IP 后点击 NEXT 进入配置界面：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476848/4.png)

<span style="font-size:16px;">选择型号之后点击 NEXT,选择 DDR3 SDRAM:</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476922/5.png)

<span style="font-size:16px;">点击 NEXT 继续进行如下配置：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476997/6.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477073/8.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477120/10.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477160/11.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477205/12.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477233/13.png)

<span style="font-size:16px;">接着点击 NEXT 按如下配置。</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477292/14.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477338/15.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477379/16.png)

<span style="font-size:16px;">

点击 validate ，再点 next 至结束。


打开工程编译下板之后，用 ILA 抓数据，先控制写入数据，再读出数据，判断是否正确。

1. 写入数据为 123456789_123456789_123456789_12345。

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477455/17.png)

<span style="font-size:16px;">

2. 读出的数据与写入一致。

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477521/18.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477567/19.png)
