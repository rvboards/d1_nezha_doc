# wujian100操作指导 #

<br>

## 一、布署到 Perf-V ##

<span style="font-size:16px;">1. 新建一个工程文件夹。</span><br>

<span style="font-size:16px;">2. 打开 vivado 并建立工程，其中注意芯片型号选择。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289239/7.png)

<span style="font-size:16px;">3. 添加 verilog 源码：注意先添加 top 文件，有两个 top 文件，一个在 fpga 目录下（用于综合实现），一个在 SOC 目录下（用于仿真），此时应该添加 fpga 目录下的 top 文件，之后添加 SOC 目录下除 top 文件的所有文件。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289345/8.png)

<span style="font-size:16px;">4.文件添加进来后，VIVADO 会自动识别、编译、分析，VIVADO 分析文件中的错误，用红色波浪线标识（错误原因是没有识别出头文件，将这四个文件类型改为头文件类型即可）。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289444/9.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289502/10.png)

<span style="font-size:16px;">5.根据 perfv 开发板手册添加管脚约束。</span><br>

<span style="font-size:16px;">6.进行综合，综合无误后进行实现</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289627/11.png)

<span style="font-size:16px;">7.实现后结果异常，需要进行时序约束，在约束文件中添加 create\_clock \-period 50.00 \-name 
MAIN\_CLK [get\_ports PIN\_EHS] 和 set\_false\_path \-from [get\_ports PIN\_EHS] \-to [get\_pins x\_cpu_top/CPU/x\_cr\_tcipif\_top/x\_cr\_coretim\_top/refclk\_ff1\_reg/D]</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289765/12.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653289827/13.png)

<span style="font-size:16px;">8.再次进行实现，没有之前的时序问题，生成 bit 流文件,并将 bit 文件烧入到开发板。</span><br>
<span style="font-size:16px;">100T:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290196/14.png)

<span style="font-size:16px;">50T:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290256/15.png)

## 二、环境搭建 ##

### 2.1ckserver 安装及配置 ###

<span style="font-size:16px;">解压 CSKY-DebugServer-windows*.zip 文件，双击运行解压出的 Setup.exe 将弹出 ckserver 安装界面，点击 next。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290387/16.png)

<span style="font-size:16px;">请认真查看 ckserver 的软件使用协议，确认后点击 yes 继续。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290451/17.png)

<span style="font-size:16px;">输入用户名和企业名称，选择用户，点击 next。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290511/18.png)

<span style="font-size:16px;">选择安装目录：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290575/19.png)

<span style="font-size:16px;">选择安装内容，其中：C-SKY Debug Proxy Server 是 C-SKY 调试代理程序；ICE Driver 是 ICE 设备驱动安装；Tutorial 是用户手册。建议全选，点击 next。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290643/20.png)

<span style="font-size:16px;">该页面将显示用户信息及安装目录，确认无误后点击 Next 开始安装。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290733/21.png)

<span style="font-size:16px;">继续下一步完成安装。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290788/22.png)

<span style="font-size:16px;">完成安装后进行参数设置：</span><br>
**<span style="font-size:16px;">(1)target 配置窗口</span><br>**
<span style="font-size:16px;">[Setting->Target Setting]打开配置信息对话框。如图所示，</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290884/23.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653290928/24.png)

<span style="font-size:16px;">其中：</span><br>


- <span style="font-size:16px;">Debug Arch Select 选择调试架构，可选择CSKY HAD和RISCV DM</span><br>
- <span style="font-size:16px;">ICE Vendor Select：选择不同厂商的ICE设备，默认为CK-Link</span><br>
- <span style="font-size:16px;">ICE Device Select(Free)：指定ICE连接</span><br>
- <span style="font-size:16px;">ICE Setting 设置为使用ICE作为连接目标时的信息，包括：ICE频率，mtcr延时</span><br>
- <span style="font-size:16px;">NReset Delay：设置NReset延时，确保ICE可以生成稳定的硬件复位（nreset）信号，单位10us，默认为1ms。</span><br>
- <span style="font-size:16px;">TReset Delay：设置TReset延时，确保ICE可以产生稳定的复位信号，用于复位HAD状态机，单位10us，默认为1.1ms。</span><br>
- <span style="font-size:16px;">Reset Wait：设置延时，确保在目标板收到复位信号后，目标板复位流程执行结束，默认50ms。</span><br>
- <span style="font-size:16px;">Use DDC：选择下载时是否使用DDC直通通道下载。</span><br>
- <span style="font-size:16px;">Enable TRST：执行Reset Target时是否执行TRST</span><br>
- <span style="font-size:16px;">LocalSemiHost：指当程序发生semihosting请求时是否由ckserver完成，默认由GDB完成。</span><br>

**<span style="font-size:16px;">(2)Socket端口设置</span><br>**
<span style="font-size:16px;">[Target Setting->Socket Setting]打开Socket端口设置对话框，如图所示:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291243/25.png)

<span style="font-size:16px;">手动输入端口号即可，默认值为 1025。</span><br>
**<span style="font-size:16px;">(3) 固件升级对话框</span><br>**
<span style="font-size:16px;">[Tools->UpgradeFirmware]打开固件升级对话框，如图所示:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291330/26.png)

<span style="font-size:16px;">选择与你的ICE设备对应的的升级文件即可，升级文件与ICE盒子类型要保持一致,具体对应如下：</span><br>

<span style="font-size:16px;">CKLINK\_LITE\_V2: cklink\_lite.hex</span><br>
<span style="font-size:16px;">CKLINK\_PRO\_V1: cklink\_v1.iic</span><br>
<span style="font-size:16px;">CKLINK\_PRO\_V2: cklink\_pro.iic</span><br>

**<span style="font-size:16px;">(4) Had 寄存器操作窗口</span><br>**

<span style="font-size:16px;">[Tools->HAD Register]打开 HAD 寄存器的操作对话框，可以进行 HAD 寄存器的读写操作如图
所示：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291467/27.png)

### 2.2 ICE 驱动安装 ###

<span style="font-size:16px;">1. 在“2.1.2节ckserver安装步骤”中，如果勾选了ICE Driver选项。那么ckserver安装过程中会将驱动相关文件拷贝到系统的目录下。</span><br>
<span style="font-size:16px;">2. 将您的ICE设备重新连接至PC，</span><br>
- <span style="font-size:16px;">如果您使用的是windows 7系统，那么设备插上后会自动安装好驱动；</span><br>
- <span style="font-size:16px;">如果您使用的是windows xp及以下系统，ICE设备重新连接后，系统会提示设备安装驱动，以CKLink-Lite V1 为例,步骤如下：</span><br>
<span style="font-size:16px;">系统弹出硬件安装向导，选择“自动安装软件”，点击下一步至完成安装</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291614/28.png)

## 三、编译下载工程 ##

<span style="font-size:16px;">1. 使用 cdk 打开并编译 project， 双击打开工程文件(例如 hello\_word 工程)</span><br>

<span style="font-size:16px;">wujian100\_open/sdk/projects/examples/hello\_word/CDK/wujian100\_openhello\_world
.cdkproj</span><br>

<span style="font-size:16px;">右键工程，选择 build，如图</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291737/29.png)

<span style="font-size:16px;">2. 运行工程</span><br>

<span style="font-size:16px;">单击“view” ， 选择“serial pane” 打开 cdk 的串口工具， 连接开发板串口右键单击serial pane 窗口，选择 settings， 并设置波特率为 115200， 如图：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291819/30.png)

<span style="font-size:16px;">3. 点击“Start/Stop Debugger”按钮 进入调试，工程运行后 Serial pane 窗口将会打印出” hello word” (程序修改为Hello Perfxlab)字符串。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291894/31.png)

<span style="font-size:16px;">运行 sdk\projects\benchmark\dhrystone 目录下的工程结果如下:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653291955/32.png)

<span style="font-size:16px;">运行 sdk\projects\benchmark\ coremark 目录下的工程结果如下</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1653292016/33.png)

