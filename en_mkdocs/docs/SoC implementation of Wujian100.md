## Purpose
<span style="font-size:16px;">Mainly complete the deployment of wujian100 SoC on FPGA. Learn to use Xilinx vivado tools.</span><br>

## Experimental procedure
### 1. Open wujian100 with Vivado

<span style="font-size:16px;">1) Create project</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955380/25.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955423/26.png)

<span style="font-size:16px;">Add the verilog source code after next:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955469/27.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955501/28.png)

<span style="font-size:16px;">Add the xdc file after clicking next</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955565/29.png)

<span style="font-size:16px;">Choose a development board</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955610/30.png)

<span style="font-size:16px;">2) After the file is added, VIVADO will automatically identify, compile, and analyze it. VIVADO analyzes the error in the file and marks it with a red wavy line (the reason for the error is that the header file is not recognized, and the four file types can be changed to the header file type)</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955669/31.png)

<span style="font-size:16px;">3) call clock IP</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955725/32.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955761/33.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955799/34.png)

### 2. Add pin constraints according to the perfv board manual
<span style="font-size:16px;">See the document "Changes to xdc" for details.</span><br>

### 3. Comprehensive project, download bit stream after the synthesis is correct

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955904/35.png)

<span style="font-size:16px;">There may be an error - a certain module is not found, just comment out this module</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955947/36.png)

<span style="font-size:16px;">The combined results are as follows:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955993/37.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956075/38.png)

### 4. Download to the development board
<span style="font-size:16px;">1) Interface to connect computer and development board</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956148/39.png)

<span style="font-size:16px;">2) Cure FLASH</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956198/40.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956230/41.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956264/42.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956292/43.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956322/44.png)

<span style="font-size:16px;">Display 5 indicates that wujian100 has been downloaded to the development board, and it can run after power-on reset.</span><br>
