### Three-color RGB-led light

<div style="width:100%;text-align:center;">

<span style="font-size:16px;">RGB-led light module installation schematic</span>
</div>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627350143/1.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627350198/2.png)


<span style="font-size:16px;">
In this example, the system comes with gpio driver to control the extended IO (i2c chip PCF8574A) Test script program /RVBoards_demo/rvboards_led/ rvboards_led.sh, the program is as follows

</span>

	/*******************************************************************/
	#!/bin/bash
	#rvboards led extending gpio control with D1
	#This example uses user mode to control rvboards led
	#gpio  system number  rvboards-rgbled
	#PP0    2020    LED1_R
	#PP1    2021    LED1_G
	#...    ...     no_led
	#PP7    2027    LED1_B

	#Apply for gpio
	echo 2020 > /sys/class/gpio/export
	echo 2021 > /sys/class/gpio/export
	echo 2027 > /sys/class/gpio/export
	#Enable gpio output function
	echo out > /sys/class/gpio/gpio2020/direction
	echo out > /sys/class/gpio/gpio2021/direction
	echo out > /sys/class/gpio/gpio2027/direction
	#Enable gpio high active
	echo 1 > /sys/class/gpio/gpio2020/active_low
	echo 1 > /sys/class/gpio/gpio2021/active_low
	echo 1 > /sys/class/gpio/gpio2027/active_low
	
	#Control the high and low level of gpio output, and control the led to flash on and off
	    echo 0 > /sys/class/gpio/gpio2020/value
	    echo 0 > /sys/class/gpio/gpio2021/value
	    echo 0 > /sys/class/gpio/gpio2027/value
	for var in {1..2..1}
	do
	    echo 1 > /sys/class/gpio/gpio2020/value
	    sleep 1
	    echo 1 > /sys/class/gpio/gpio2021/value
	    sleep 1
	    echo 1 > /sys/class/gpio/gpio2027/value
	    sleep 1
	    echo 0 > /sys/class/gpio/gpio2020/value
	    sleep 1
	    echo 0 > /sys/class/gpio/gpio2021/value
	    sleep 1
	    echo 0 > /sys/class/gpio/gpio2027/value
	    sleep 1
	done
	#Log off gpio
	echo 2020 > /sys/class/gpio/unexport
	echo 2021 > /sys/class/gpio/unexport
	/********************************************************************/

<span style="font-size:16px;">
Test command:

Add execute permission: chmod +x rvboards_led.sh

Execute the script program as follows：. /rvboards_led.sh, you can observe the blinking color change of the led, as follows
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627350398/3.png)
