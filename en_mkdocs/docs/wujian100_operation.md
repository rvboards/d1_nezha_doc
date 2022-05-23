# wujian100 operation guide #

<br>

## I. Deploy to Perf-V ##

<span style="font-size:16px;">1. Create a new project folder.</span><br>

<span style="font-size:16px;">2. Open vivado and create a project, paying attention to the chip model selection.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289239/7.png)

<span style="font-size:16px;">3. Add verilog source code: pay attention to add the top file first. There are two top files, one in the fpga directory (for comprehensive implementation) and one in the SOC directory (for simulation). At this time, you should add top in the fpga directory file, and then add all files in the SOC directory except the top file.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289345/8.png)

<span style="font-size:16px;">4. After the file is added, VIVADO will automatically identify, compile, and analyze it. VIVADO analyzes the errors in the file and marks them with a red wavy line (the reason for the error is that the header file is not recognized, and the four file types can be changed to the header file type).</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289444/9.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289502/10.png)

<span style="font-size:16px;">5. Add pin constraints according to the perfv development board manual.</span><br>

<span style="font-size:16px;">6. Synthesize and realize after the synthesis is correct</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289627/11.png)

<span style="font-size:16px;">7. If the result is abnormal after implementation, timing constraints need to be performed, and create\_clock \-period 50.00 \-name MAIN\_CLK [get\_ports PIN\_EHS] 和 set\_false\_path \-from [get\_ports PIN\_EHS] \-to [get\_pins x\_cpu_top/CPU/x\_cr\_tcipif\_top/x\_cr\_coretim\_top/refclk\_ff1\_reg/D] is added to the constraint file.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289765/12.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289827/13.png)

<span style="font-size:16px;">8. Implement again, without the previous timing problem, generate a bit stream file, and burn the bit file into the development board.</span><br>
<span style="font-size:16px;">100T:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290196/14.png)

<span style="font-size:16px;">50T:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290256/15.png)

## II. Environment Construction ##

### 2.1 ckserver installation and configuration ###

<span style="font-size:16px;">Unzip the CSKY-DebugServer-windows*.zip file, double-click to run the extracted Setup.exe, and the ckserver installation interface will pop up, click next.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290387/16.png)

<span style="font-size:16px;">Please check the software usage agreement of ckserver carefully, and click yes to continue after confirming.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290451/17.png)

<span style="font-size:16px;">Enter the user name and company name, select the user, and click next.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290511/18.png)

<span style="font-size:16px;">Select the installation directory:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290575/19.png)

<span style="font-size:16px;">Select the installation content, among which: C-SKY Debug Proxy Server is the C-SKY debug proxy program; ICE Driver is the ICE device driver installation; Tutorial is the user manual. It is recommended to select all and click next.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290643/20.png)

<span style="font-size:16px;">This page will display the user information and installation directory, click Next to start the installation after confirmation.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290733/21.png)

<span style="font-size:16px;">Continue to the next step to complete the installation.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290788/22.png)

<span style="font-size:16px;">After the installation is complete, set the parameters:</span><br>
**<span style="font-size:16px;">(1) target configuration window</span><br>**
<span style="font-size:16px;">[Setting->Target Setting] opens the Configuration Information dialog. as the picture shows,</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290884/23.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290928/24.png)

<span style="font-size:16px;">In:</span><br>


- <span style="font-size:16px;">Debug Arch Select Select debug architecture, select CSKY HAD and RISCV DM</span><br>
- <span style="font-size:16px;">ICE Vendor Select: Select ICE devices from different manufacturers, the default is CK-Link</span><br>
- <span style="font-size:16px;">ICE Device Select(Free)：Specify ICE connection</span><br>
- <span style="font-size:16px;">ICE Setting is set to use ICE as the connection target information, including: ICE frequency, mtcr delay</span><br>
- <span style="font-size:16px;">NReset Delay: Set the NReset delay to ensure that the ICE can generate a stable hardware reset (nreset) signal, the unit is 10us, and the default is 1ms.</span><br>
- <span style="font-size:16px;">TReset Delay: Set the TReset delay to ensure that the ICE can generate a stable reset signal to reset the HAD state machine, the unit is 10us, and the default is 1.1ms.</span><br>
- <span style="font-size:16px;">Reset Wait: Set the delay to ensure that the reset process of the target board ends after the target board receives the reset signal. The default is 50ms.</span><br>
- <span style="font-size:16px;">Use DDC: Select whether to use the DDC pass-through channel for downloading.</span><br>
- <span style="font-size:16px;">Enable TRST: Whether to execute TRST when Reset Target is executed</span><br>
- <span style="font-size:16px;">LocalSemiHost：Refers to whether the program is completed by ckserver when a semihosting request occurs, and it is completed by GDB by default.</span><br>

**<span style="font-size:16px;">(2) Socket port settings</span><br>**
<span style="font-size:16px;">[Target Setting->Socket Setting] open the Socket Port Settings dialog box, as shown in the figure:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291243/25.png)

<span style="font-size:16px;">Enter the port number manually, the default value is 1025.</span><br>
**<span style="font-size:16px;">(3) Firmware upgrade dialog</span><br>**
<span style="font-size:16px;">[Tools->UpgradeFirmware] open the firmware upgrade dialog box, as shown in the figure:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291330/26.png)

<span style="font-size:16px;">Just select the upgrade file corresponding to your ICE device. The upgrade file must be consistent with the type of ICE box. The specific correspondence is as follows:</span><br>

<span style="font-size:16px;">CKLINK\_LITE\_V2: cklink\_lite.hex</span><br>
<span style="font-size:16px;">CKLINK\_PRO\_V1: cklink\_v1.iic</span><br>
<span style="font-size:16px;">CKLINK\_PRO\_V2: cklink\_pro.iic</span><br>

**<span style="font-size:16px;">(4) Had register operation window</span><br>**

<span style="font-size:16px;">[Tools->HAD Register] open the operation dialog of the HAD register, you can read and write the HAD register as shown in the figure:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291467/27.png)

### 2.2 ICE driver installation ###

<span style="font-size:16px;">1. In "2.1.2 ckserver installation steps", if the ICE Driver option is checked. Then the ckserver installation process will copy the driver related files to the system directory.</span><br>
<span style="font-size:16px;">2. Reconnect your ICE device to the PC,</span><br>
- <span style="font-size:16px;">If you are using the Windows 7 system, the driver will be automatically installed after the device is plugged in;</span><br>
- <span style="font-size:16px;">If you are using Windows XP or below, after the ICE device is reconnected, the system will prompt the device to install the driver. Take CKLink-Lite V1 as an example, the steps are as follows:</span><br>
<span style="font-size:16px;">The system pops up the hardware installation wizard, select "Automatically install the software", click Next to complete the installation</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291614/28.png)

## III. Compile and download the project ##

<span style="font-size:16px;">1. Use cdk to open and compile the project, double-click to open the project file (such as the hello\_word project)</span><br>

<span style="font-size:16px;">wujian100\_open/sdk/projects/examples/hello\_word/CDK/wujian100\_openhello\_world
.cdkproj</span><br>

<span style="font-size:16px;">Right-click the project and select build, as shown in the figure</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291737/29.png)

<span style="font-size:16px;">2. Run the project</span><br>

<span style="font-size:16px;">Click "view", select "serial pane" to open the serial port tool of cdk, connect the serial port of the development board, right-click the serial pane window, select settings, and set the baud rate to 115200, as shown in the figure:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291819/30.png)

<span style="font-size:16px;">3. Click the "Start/Stop Debugger" button to start debugging, and the Serial pane window will print out the string "hello word" (the program is modified to Hello Perfxlab) after the project is running.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291894/31.png)

<span style="font-size:16px;">The results of running the project in the sdk\projects\benchmark\dhrystone directory are as follows:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291955/32.png)

<span style="font-size:16px;">The results of running the project in the sdk\projects\benchmark\ coremark directory are as follows</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653292016/33.png)

