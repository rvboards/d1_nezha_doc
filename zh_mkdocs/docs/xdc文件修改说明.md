**<span style="font-size:16px;">说明：修改xdc文件（即该芯片的约束文件），要配置成所用板子一致的xdc</span><br>**
**<span style="font-size:16px;">需要的资料：</span>**<span style="font-size:16px;">开发板用户手册；wujian100工程里的xdc文件</span><br>

### 1. 开发板用户手册重点阅读内容
<span style="font-size:16px;">1) 时钟：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543491/57.png)

<span style="font-size:16px;">2) IO口电压：不同开发板用的电压不一样</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543535/58.png)

<span style="font-size:16px;">设置电压的约束：</span><br>
<span style="font-size:16px;">set_property CONFIG_VOLTAGE 3.3 [current_design] ：全部设定电压为3.3</span><br>

<span style="font-size:16px;">3) 引脚：以灯和开关为例子：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543615/59.png)

<span style="font-size:16px;">4) Flash</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543673/60.png)

<span style="font-size:16px;">5) 接口：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543758/61.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543791/62.png)

<span style="font-size:16px;">两种接口区别：</span><br>
<span style="font-size:16px;">UART：是嵌入式开发所说的串口。通过它可以向设备烧写程序和调试程序。</span><br>
<span style="font-size:16px;">JTAG：用于设备调试，需要硬件支持。主要用于芯片内部测试，调试程序。可以直接观察和修改寄存器和内存中的数据，方便找出程序中的问题。</span><br>

### 2. xdc约束更改
<span style="font-size:16px;">1) 时钟：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543909/63.png)

<span style="font-size:16px;">set_property CLOCK_DEDICATED_ROUTE FALSE [get_nets PAD_JTAG_TCLK]</span><br>
<span style="font-size:16px;">这一句必须加上</span><br>

<span style="font-size:16px;">2) LED：</span><br>
<span style="font-size:16px;">注意这三列，对照开发板资料给的引脚改</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543993/64.png)

<span style="font-size:16px;">3) 复位:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544046/65.png)

<span style="font-size:16px;">4) UART JTAG：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544085/66.png)

<span style="font-size:16px;">5) JTAG：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544133/67.png)

<span style="font-size:16px;">6) SD卡：</span><br>
<span style="font-size:16px;">注意这两列，对照开发板资料给的引脚改</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544204/68.png)

### 3. 其他

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544256/69.png)

<span style="font-size:16px;">这些根据自己板子的资源多少和想实现的功能改；比如只想实现点灯，那么这些就可以全注释掉；但如果要实现OLED，那先看自己板子有没有OLED的配置，然后根据开发板手册改xdc里相对应的引脚；</span><br>
<span style="font-size:16px;">以下为移植到A7 50T的xdc代码：</span><br>

	set_property IOSTANDARD LVCMOS33 [get_ports]  
	
	#clock
	set_property -dict {PACKAGE_PIN N14 IOSTANDARD LVCMOS33} [get_ports clk]
	create_clock -period 20.000 -name sys_clk_pin -waveform {0.000 10.000} -add [get_ports clk]
	
	set_property CLOCK_DEDICATED_ROUTE FALSE [get_nets PAD_JTAG_TCLK]
	
	#LED
	set_property -dict {PACKAGE_PIN N16 IOSTANDARD LVCMOS33} [get_ports PAD_GPIO_0]
	set_property -dict {PACKAGE_PIN P15 IOSTANDARD LVCMOS33} [get_ports PAD_GPIO_1]
	set_property -dict {PACKAGE_PIN P16 IOSTANDARD LVCMOS33} [get_ports PAD_GPIO_2]
	
	#RESET button
	set_property PACKAGE_PIN L13 [get_ports PAD_MCURST]
	
	#USI0
	set_property PACKAGE_PIN T7 [get_ports PAD_USI0_SCLK]
	set_property PACKAGE_PIN T8 [get_ports PAD_USI0_SD0]
	
	
	#JTAG
	set_property PACKAGE_PIN F12 [get_ports PAD_JTAG_TCLK]
	set_property PACKAGE_PIN F13 [get_ports PAD_JTAG_TMS]
	
	#SD card
	set_property PACKAGE_PIN L4 [get_ports { PAD_GPIO_6 }]; #Sch=sd_cclk         sclk        PAD_GPIO_6
	set_property PACKAGE_PIN T2 [get_ports { PAD_GPIO_18 }]; #Sch=sd_cd          card detect
	set_property PACKAGE_PIN R1 [get_ports { PAD_GPIO_5 }]; #Sch=sd_cmd          mosi        PAD_GPIO_5
	set_property PACKAGE_PIN H16 [get_ports { PAD_GPIO_7 }]; #Sch=sd_d[0]         miso        PAD_GPIO_7
	set_property PACKAGE_PIN R2 [get_ports { PAD_GPIO_19 }]; #Sch=sd_d[3]        cs          PAD_GPIO_19
	# set_property PACKAGE_PIN F12 [get_ports { PAD_GPIO_20 }]; #Sch=sd_reset       rst         PAD_GPIO_20
	
	set_property CFGBVS VCCO [current_design]
