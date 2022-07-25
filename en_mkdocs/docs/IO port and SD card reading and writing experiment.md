## Experimental goal
<span style="font-size:16px;">(1) After the wujian100 SoC is deployed on the FPGA, set the I/O pin of the SoC to high or low level, observe the on and off of the LED, and learn to use the I/O of the E902.</span><br>
<span style="font-size:16px;">(2) Learn to use the E902 processor to read and write SD cards, which requires SD cards and SD card expansion boards.</span><br>
<span style="font-size:16px;">Note: SD card related functions require Pref's SD card expansion board, and the sockets are as follows. The program of the SD card and the program of the LED are together, so they can be tested together.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193358/1.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193395/2.png)

## Experimental procedure
### 1. Connect the computer and wujian100
<span style="font-size:16px;">Clink and PMOD connection:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193460/3.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193503/5.png)

<span style="font-size:16px;">The corresponding relationship is as follows:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193549/6.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193583/7.png)

### 2. Connect the USB-to-serial downloader and develop

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193634/8.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193675/9.png)

### 3. Compile and debug

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193722/10.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193751/11.png)

<span style="font-size:16px;">The next step can be performed only when E902 is displayed. If it is not displayed, you can check whether the connection between PMOD and CLINK is wrong, or not connected.</span><br>

### 4. CDK's serial port window

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193808/12.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193846/13.png)

### 5. Download the program

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193889/14.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193919/15.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193950/16.png)

<span style="font-size:16px;">Or use these two:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193992/17.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658194029/18.png)

### 6. After reset, the correct phenomenon is that the light flashes, and

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658194073/19.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658194100/20.png)

<span style="font-size:16px;">Indicates that the SD card is read correctly, and you can view the specific value in the register on the Debug interface.</span><br>
