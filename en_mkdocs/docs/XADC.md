### XADC

**<span style="font-size:16px;">Project name：</span>**<span style="font-size:16px;">XADC Usage.</span>

**<span style="font-size:16px;">Specific requirements：</span>**<span style="font-size:16px;">Implement the xadc's ip core to collect input data and output the sampling results.</span>

**<span style="font-size:16px;">System Design：</span>**
<span style="font-size:16px;">The Artix-7 series FPGA contains two 12-bit, 1 MSPS analog-to-digital converters that can be configured to sample two external analog channels simultaneously. The development board uses an on-chip reference voltage of 1.25 V for the AD sampling part, and the on-chip reference voltage has good stability. p1 high-speed socket contains two pairs of high-speed differential input AD sampling; p2 is Arduino compatible and contains six single-ended inputs or six pairs of differential input AD sampling.</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627984931/22.png)

**<span style="font-size:16px;">Implementation process：</span>**

<span style="font-size:16px;">

1. initialize the ip core of xadc and connect the development board.

2. Open the vivado file for comprehensive download, download the jtag with the connection, and double-click on the Xadc in the figure.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627985051/23.png)

<span style="font-size:16px;">

3. open and add the data to be tested, at this time the A5 pin is connected to the external voltage, the input voltage 2.0 volts test result is shown in the figure: (VAUXP1_VAUXP2 is the corresponding channel), because the circuit diagram uses voltage division, so the test result is 3.32 parts per million of the voltage under test.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627985185/24.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627985282/25.png)

<span style="font-size:16px;">

The correspondence between the ad channels in the development version and the development version is shown below.

</span>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1627985420/26.png)


