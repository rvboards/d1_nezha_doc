**<span style="font-size:16px;">Description: Modify the xdc file (that is, the constraint file of the chip), and configure it to the same xdc for the board used</span><br>**
**<span style="font-size:16px;">Required information:</span>**<span style="font-size:16px;">Development board user manual; xdc file in the wujian100 project</span><br>

### 1. Key reading content of the development board user manual
<span style="font-size:16px;">1) Clock:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543491/57.png)

<span style="font-size:16px;">2) IO port voltage: different development boards use different voltages</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543535/58.png)

<span style="font-size:16px;">Set the constraints for the voltage:</span><br>
<span style="font-size:16px;">set_property CONFIG_VOLTAGE 3.3 [current_design] : All set voltages to 3.3</span><br>

<span style="font-size:16px;">3) Pins: Take lights and switches as examples:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543615/59.png)

<span style="font-size:16px;">4) Flash</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543673/60.png)

<span style="font-size:16px;">5) Interface:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543758/61.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543791/62.png)

<span style="font-size:16px;">The difference between the two interfaces:</span><br>
<span style="font-size:16px;">UART: It is the serial port called by embedded development. Through it, you can program and debug programs to the device.</span><br>
<span style="font-size:16px;">JTAG: Used for device debugging and requires hardware support. Mainly used for chip internal testing, debugging programs. You can directly observe and modify the data in registers and memory, which is convenient to find out the problems in the program.</span><br>

### 2. xdc constraint changes
<span style="font-size:16px;">1) Clock:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543909/63.png)

<span style="font-size:16px;">set_property CLOCK_DEDICATED_ROUTE FALSE [get_nets PAD_JTAG_TCLK]</span><br>
<span style="font-size:16px;">This sentence must be added</span><br>

<span style="font-size:16px;">2) LED:</span><br>
<span style="font-size:16px;">Pay attention to these three columns, and change the pins according to the data of the development board.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658543993/64.png)

<span style="font-size:16px;">3) Reset:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544046/65.png)

<span style="font-size:16px;">4) UART JTAG：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544085/66.png)

<span style="font-size:16px;">5) JTAG：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544133/67.png)

<span style="font-size:16px;">6) SD card：</span><br>
<span style="font-size:16px;">Pay attention to these two columns, and change the pins according to the data of the development board.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544204/68.png)

### 3. Other

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658544256/69.png)

<span style="font-size:16px;">These can be changed according to the resources of your board and the functions you want to achieve; for example, if you only want to realize the lighting, then these can be fully commented out; but if you want to implement OLED, first check whether your board has OLED configuration, and then according to the development board manual Change the corresponding pin in xdc;</span><br>
<span style="font-size:16px;">The following is the xdc code ported to the A7 50T:</span><br>

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
