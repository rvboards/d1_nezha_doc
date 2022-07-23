## Purpose
<span style="font-size:16px;">Wujian100_open is an open source RISC-V project by Ali Pingtou on Github. This document simulates Wujian100 in Linux environment.</span><br>

## Experimental procedure
### 1. Download the official code
<span style="font-size:16px;">The emulation of No Sword requires a Linux environment. Here, the SSH terminal of MobaXterm is used to connect to the Ubuntu workstation.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953226/5.png)

<span style="font-size:16px;">Create a folder as the project folder: mkdir wujian</span><br>
<span style="font-size:16px;">Change the working directory to this folder: cd wujian</span><br>
<span style="font-size:16px;">Download Wujian100's code from github to this folder: git clone http://github.com/T-head-Semi/wujian100_open.git</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953291/6.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953313/7.png)

### 2. Download the toolchain
<span style="font-size:16px;">Download the toolchain on the official website of Pingtouge. The version may be different, just download the latest one.</span><br>
<span style="font-size:16px;">Address:https://occ.t-head.cn/community/download?id=3913221581316624384</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953398/8.png)

<span style="font-size:16px;">Create the toolchain folder: mkdir riscv_toolchain</span><br>
<span style="font-size:16px;">Change the working directory to this folder: cd riscv_toolchain</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953440/9.png)

<span style="font-size:16px;">Put the downloaded toolchain zip file in this folder, drag and drop the file directly here, and upload the file from the Windows machine to the workstation of the Ubuntu system. You can also use the cp copy command to copy to the folder.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953497/10.png)

<span style="font-size:16px;">Unzip files: tar -zxvf riscv64-elf-x86_64-20210512.tar.gz</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953547/11.png)

<span style="font-size:16px;">Wait for the decompression to complete.</span><br>

### 3. Modify the script
<span style="font-size:16px;">Since the original script is the setup.csh file, there are some incompatibilities in the bash environment. Here is a new setup.sh script, as shown in the figure below, put it in the wujian100_open/tools directory (original setup.csh directory)</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953631/12.png)

<span style="font-size:16px;">Cd to wujian100_open/tools directory:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953676/13.png)

<span style="font-size:16px;">Here is also to upload the setup.sh file of the Windows machine to the workstation.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953741/14.png)

<span style="font-size:16px;">Input: source setup.sh</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953775/15.png)

### 4. Run the simulation
<span style="font-size:16px;">Go to the wujian100_open/workdir directory to run the simulation: cd ../workdir</span><br>
<span style="font-size:16px;">Start running the simulation: ../tools/run_case -sim_tool iverilog ../case/timer/timer_test.c</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953836/16.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953864/17.png)

<span style="font-size:16px;">Simulation succeeded</span><br>

### 5. View the simulation waveform
<span style="font-size:16px;">After running the simulation, test.vcd will be generated in the wujian100_open/workdir directory, as shown in the following figure. The VCD file contains the change information of the signal, which is equivalent to recording the information of the entire simulation. We can use this file to reproduce the simulation and display the waveform.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953929/18.png)

<span style="font-size:16px;">Because VCD is part of the Verilog HDL language standard, all verilog simulators can view this file.</span><br>
<span style="font-size:16px;">Here is an introduction to viewing waveforms with Modelsim software. Transfer the generated test.vcd file to the Windows host and store it in the E:/Project/wujian100_sim folder.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953991/19.png)

<span style="font-size:16px;">Open the Modelsim software</span><br>
<span style="font-size:16px;">Click File->Change Directory to change the directory to the directory of test.vcd; or directly enter the console in Modelsim: cd E:/Project/wujian100_sim to directly set it to this folder.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657954040/20.png)

<span style="font-size:16px;">Because Modelsim only supports .wlf waveform files, format conversion is required.</span><br>
<span style="font-size:16px;">In the console in Modelsim enter: vcd2wlf test.vcd test.wlf</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657954084/21.png)

<span style="font-size:16px;">Open test.wlf in Modelsim, click File->Open->test.wlf</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657954126/22.png)

<span style="font-size:16px;">Select the signal to be observed in the object tab and add it to the waveform window.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657954187/23.png)
