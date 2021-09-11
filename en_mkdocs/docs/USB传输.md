### USB Transfer

**<span style="font-size:16px;">Project name：</span>**<span style="font-size:16px;">USB transfer.</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">complete USB data transfer based on PERF-V development board.</span>

<span style="font-size:16px;">
A high-speed port to 2.54 interface adapter board is used in the design, and the detailed design is as follows.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069608/90.png)

**<span style="font-size:16px;">Implementation process：</span>**

<span style="font-size:16px;">
1 installation of USB2.0 module development software: the development of this USB2.0 module, you need to use two software, respectively CySuiteUSB_3_4_5_B192.exe and ez_usb_fx2lp_development_kit.exe", just double-click the installation package, and all the way to select Next to complete the installation.

2 Install the standard driver for this USB2.0 module：Before this module can be recognized by the computer and read and write data normally, the driver needs to be installed. As most of the users' computers are currently on win7 or higher, the installation of this module on win7 and above requires verification of the driver signature. The official driver is not verified by the driver signature, so we need to turn off the driver signature of the system.

Use the USB cable to connect the USB module to the USB port of the computer, at this time, the system should pop up in the lower right corner to find new hardware, and the driver installation failed.

Check the Device Manager, you should see an unknown device as shown below, we select the device and click the right mouse button to view its details. In the Details column, we select "Hardware ID" in the Properties drop-down table and see that the value is USB\VID_040B&PID_8613, which is the hardware ID of our USB2.0 module.

Switch to the Driver tab and select 'Update Driver', as shown below.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069776/91.png)

<span style="font-size:16px;">
In the pop-up screen, select "Browse Computer for Driver Software" and locate the path to the driver installation path of the USB development kit we provided, then click OK.

Then click Next and the screen will pop up as shown below, click Always Install.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069847/92.png)

<span style="font-size:16px;">
Then we go back to the Device Manager, under Universal Serial Bus Controller, you can see the device as shown below, and no exclamation point to indicate an exception, then the driver is installed correctly.
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069902/93.png)

<span style="font-size:16px;">
3 Burn the USB2.0 chip firmware

Next, we open the CyConsole EZ-USB software to burn the USB block transfer firmware we use for testing. Once the software is open, we can see our Cypress USB XXX device in the Device column, as shown in the following figure.
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628069974/94.png)

<span style="font-size:16px;">
Next, we click on the Lg EEPROM button, which will open the file selection box, then locate the location where we provided the USB chip firmware, select the bulkloop.iic file, double click on it to open it and automatically start the firmware download.

After the firmware download is complete, disconnect the USB cable and reconnect it, then in the Device window of the interface you can see that the device name has changed to REIMU, then we switch to the Cypress USB Console software and see that the device has been found.
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628070045/95.png)

<span style="font-size:16px;">
4 FPGA write USB test

Download the FPGA program to the development board, go back to the Cypress USB Console tool, switch to the Other Endpt Xfers option, then select 0x86(in), change Bytes of Data to 1024, then click the Transfer Data button, then you can see the received data in the Console, and compare with the actual data sent. Then you can see the received data in the Console and check it with the actual data sent.
</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1628070119/96.png)

<span style="font-size:16px;">
The data is organized in such a way that two consecutive 8-bit pieces of data form a 16-bit piece of data. For example, the last line of the received data, 01 F9, is combined to make 505, and the last 02 00 is combined to make 512. Since our test project is sending from 1 to 512 in succession, we know that the data is transmitted correctly.
</span>


