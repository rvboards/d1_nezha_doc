## 实验目的
<span style="font-size:16px;">Wujian100_open是阿里平头哥在Github上开源了RISC-V项目。本文档在Linux环境下进行Wujian100的仿真。</span><br>

## 实验步骤
### 1. 下载官方代码
<span style="font-size:16px;">无剑的仿真需要Linux环境，这里使用的是MobaXterm的SSH终端连接Ubuntu的工作站。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953226/5.png)

<span style="font-size:16px;">建一个文件夹，作该为项目的文件夹：mkdir wujian</span><br>
<span style="font-size:16px;">切换工作目录到该文件夹下：cd wujian</span><br>
<span style="font-size:16px;">将Wujian100的代码从github上下载到该文件夹下: git clone http://github.com/T-head-Semi/wujian100_open.git</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953291/6.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953313/7.png)

### 2. 下载工具链
<span style="font-size:16px;">在平头哥的官网上下载工具链。版本可能不同，下载最新的就好。</span><br>
<span style="font-size:16px;">地址：https://occ.t-head.cn/community/download?id=3913221581316624384</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953398/8.png)

<span style="font-size:16px;">创建工具链文件夹：mkdir riscv_toolchain</span><br>
<span style="font-size:16px;">切换工作目录到该文件夹下：cd riscv_toolchain</span><br>

![](./images_dir/1657953440/9.png)

<span style="font-size:16px;">将下载好的工具链压缩包放到该文件夹下，这里直接拖拽复制，将文件由Windows本机上传到了该Ubuntu 系统的工作站上。也可用cp复制命令复制到文件夹下。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953497/10.png)

<span style="font-size:16px;">解压文件：tar -zxvf riscv64-elf-x86_64-20210512.tar.gz</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953547/11.png)

<span style="font-size:16px;">等待解压完成。</span><br>

### 3. 修改脚本
<span style="font-size:16px;">由于原本的脚本是setup.csh文件，在bash环境下有一些不兼容的地方。这里重新建立一个setup.sh脚本，如下图所示，放入wujian100_open/tools目录下(原setup.csh目录)</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953631/12.png)

<span style="font-size:16px;">Cd 到wujian100_open/tools目录下：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953676/13.png)

<span style="font-size:16px;">这里也是将Windows本机的setup.sh文件上传到工作站上。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953741/14.png)

<span style="font-size:16px;">输入： source setup.sh</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953775/15.png)

### 4. 运行仿真
<span style="font-size:16px;">进入到wujian100_open/workdir目录下运行仿真：cd ../workdir</span><br>
<span style="font-size:16px;">开始运行仿真： ../tools/run_case -sim_tool iverilog ../case/timer/timer_test.c</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953836/16.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953864/17.png)

<span style="font-size:16px;">仿真成功</span><br>

### 5. 仿真波形的查看
<span style="font-size:16px;">在运行完仿真后，在wujian100_open/workdir目录下会生成test.vcd，如下图所示。VCD文件包含了信号的变化信息，就相当于记录了整个仿真的信息，我们可以用这个文件来再现仿真，也就能够显示波形。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953929/18.png)

<span style="font-size:16px;">因为VCD是 Verilog HDL语言标准的一部分，因此所有的verilog的仿真器都能够查看该文件。</span><br>
<span style="font-size:16px;">这里介绍用Modelsim软件查看波形。将生成的test.vcd文件传输到Windows主机上，存放于E:/Project/wujian100_sim文件夹下。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657953991/19.png)

<span style="font-size:16px;">打开Modelsim软件</span><br>
<span style="font-size:16px;">点击File->Change Directory，将目录更改至test.vcd的目录下；或者直接在在Modelsim中的控制台输入：cd E:/Project/wujian100_sim 直接定为到该文件夹下。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657954040/20.png)

<span style="font-size:16px;">因为Modelsim只支持.wlf波形文件，所以需要做格式转换。</span><br>
<span style="font-size:16px;">在Modelsim中的控制台输入：vcd2wlf test.vcd test.wlf</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657954084/21.png)

<span style="font-size:16px;">在Modelsim中打开test.wlf，点击File->Open->test.wlf</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657954126/22.png)

<span style="font-size:16px;">在object标签中选取需要观察的信号添加到波形窗即可。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657954187/23.png)
