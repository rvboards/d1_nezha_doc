### DDR3

<span style="font-size:16px;">

This development board is equipped with a high-speed DDR3 SDRAM, model: MT41J128M16JT-093, capacity: 256MByte (128M*16bit), 16bit bus. The FPGA and DDR3 SDRAM on the development board are connected to the BANK35 IO. The DDR3 hardware design requires strict consideration of signal integrity, and we have fully considered matching resistors/termination resistors, alignment impedance control, and alignment equal length control during the circuit design and PCB design to ensure the high speed and stable operation of DDR3.

</span>

**<span style="font-size:16px;">Project：</span>**<span style="font-size:16px;">DDR3。</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">implement DDR3 data reading and writing.</span>

**<span style="font-size:16px;">System design：</span>**

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476573/1.png)

**<span style="font-size:16px;">Implementation process：</span>**

<span style="font-size:16px;">1.After creating a new project, open Create Block Design, and modify the Design name.</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476665/2.png)

<span style="font-size:16px;">
2.Add IPs and complete the connection according to the system design.
  
3.Follow the diagram below to configure the IP accordingly.
</span>

**<span style="font-size:16px;">Axi Datamover Configuration：</span>**

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476756/3.png)

**<span style="font-size:16px;">mig_7_series Configuration：</span>**

<span style="font-size:16px;">After opening the IP, click NEXT to enter the configuration interface.</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476848/4.png)

<span style="font-size:16px;">After selecting the model, click NEXT and select DDR3 SDRAM:</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476922/5.png)

<span style="font-size:16px;">Click NEXT to continue with the configuration as follows.：</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627476997/6.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477073/8.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477120/10.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477160/11.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477205/12.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477233/13.png)

<span style="font-size:16px;">Then click NEXT to configure as follows.</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477292/14.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477338/15.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477379/16.png)

<span style="font-size:16px;">

Click on validate and then click next to finish.


Open the project and compile the board, then use ILA to capture the data, first control the write data, then read the data to determine if it is correct.

1. The write data is 123456789_123456789_123456789_12345。

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477455/17.png)

<span style="font-size:16px;">

2. The read data is the same as the write.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477521/18.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627477567/19.png)
