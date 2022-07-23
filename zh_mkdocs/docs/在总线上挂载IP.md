## 实验目标
<span style="font-size:16px;">Wujian100中有留有许多dummy模块，可供用户自定义设计。本文档使用AHB总线上的Dummy0模块，通过写寄存器的方式控制RGB LED外设。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539100/1.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539132/2.png)

<span style="font-size:16px;">本次实验在vivado中建立自己的IP，IP为AXI4接口。基于三色LED灯的控制需要9位，这里用32位寄存器0的低9位作为控制输出。挂载IP到wujian100、实现与验证功能。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539182/3.png)

## 实验步骤
### 1. 建立Block Design
<span style="font-size:16px;">Wujian100软核为AHB总线，VIVADO支持 AXI总线IP，需要用到AHB-Lite to AXI Bridge转接模块。</span><br>
<span style="font-size:16px;">点击Create Block Design，输入设计名，打开Block Design界面。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539305/4.png)

<span style="font-size:16px;">点击加号添加IP，搜索AHB-Lite to AXI Bridge，选择双击添加。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539359/5.png)

<span style="font-size:16px;">点击模块，按图标或Ctrl+T引出端口。该桥接模块作为AXI主机，自定义IP为AXI从机。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539419/6.png)

<span style="font-size:16px;">后面需要对源文件中的端口名进行修改，这里将后缀去掉，待会编辑的时候方便一点</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539506/7.png)

<span style="font-size:16px;">创建自己的AXI IP核，自定义AXI IP。点击Tools->Create and Package New IP。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539580/8.png)

<span style="font-size:16px;">点击Next。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539633/9.png)

<span style="font-size:16px;">选择创建AXI外围的IP，点击Next。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539683/10.png)

<span style="font-size:16px;">可对IP自己命名，写描述。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539734/11.png)

<span style="font-size:16px;">桥是master ，我们就创建slave的模式。如下图，点击Next。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539786/12.png)

<span style="font-size:16px;">点击左侧IP Catalog，打开IP管理器，看到刚才添加的myio→ 右击myio_v1.0 → Edit in IP Packager选项，单击OK，此时系统会自动打开另一个Vivado IDE来对用户IP核进行编辑。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539834/13.png)

<span style="font-size:16px;">在本模块中，设定有4个寄存器，每个寄存器位宽 32 位。这里通过往寄存器中写数据，来达到控制输出端口电平，从而控制三色灯的输出。将输出端口连接寄存器寄存器。</span><br>
<span style="font-size:16px;">双击进入myio_v1_0_S00_AXI，设计文件里面有用户代码区域。</span><br>
<span style="font-size:16px;">根据需求增加端口声明和添加用户信号。这里增加一个output [31:0]myio用于控制三色灯。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539917/14.png)

<span style="font-size:16px;">根据需求，添加用户逻辑代码。这里增加assign myio = slv_reg0; 将输出连上寄存器0。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539971/15.png)

<span style="font-size:16px;">双击击进入IP的顶层，增加output [31:0]myio</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540029/16.png)

<span style="font-size:16px;">例化中增加.myio(myio),</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540076/17.png)

<span style="font-size:16px;">将更改刷新。切换到Package IP-myio窗口，单击如图所示链接，对刚才修改过的顶层文件进行更新。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540130/18.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540166/19.png)

<span style="font-size:16px;">重新打包一下IP</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540225/20.png)

<span style="font-size:16px;">现在可以使用这个IP了，将IP添加进Block Design。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540284/21.png)

<span style="font-size:16px;">但它们的AXI port仍然有点差异，连接不上，需要加一个互联的IP</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540340/22.png)

<span style="font-size:16px;">添加AXI Interconnect模块</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540388/23.png)

<span style="font-size:16px;">双击打开AXI Interconnect模块，Slave和Master的接口都为1。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540439/24.png)

<span style="font-size:16px;">可以鼠标拖拽，连接端口</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540498/25.png)

<span style="font-size:16px;">直接点击自动连接</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540543/26.png)

<span style="font-size:16px;">自动连接所以，点击确定。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540589/27.png)

<span style="font-size:16px;">在自动布线后，出现了一个新的模块连接rst信号，这里把它删掉，自己手动连接。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540644/28.png)

<span style="font-size:16px;">将reset信号手动连好。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540699/29.png)

<span style="font-size:16px;">选中myio模块，ctrl+t引出输出</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540765/30.png)

<span style="font-size:16px;">与之前一样修改名称，改为myio</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540811/31.png)

<span style="font-size:16px;">分配地址。去Adress Editor界面，找到myio_0，右键点击Assign。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540858/32.png)

<span style="font-size:16px;">将地址修改为dummy0的首地址0x4001_0000。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540925/33.png)

<span style="font-size:16px;">回到diagram窗口，点击验证一下，没有错误，退出block design。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540978/34.png)

### 2. 挂IP到wujian100
<span style="font-size:16px;">生成IP的Wrapper。在Source里找到生成的ahb_axi，右键Generate Output Products</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541046/35.png)

<span style="font-size:16px;">再右键点击Create HDL Wrapper。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541090/36.png)

<span style="font-size:16px;">点击OK。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541131/37.png)

<span style="font-size:16px;">可以看到生成了wrapper，可以被调用，或者再加一层文件进行调用。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541194/38.png)

<span style="font-size:16px;">给自己的design加一层顶层文件。点击+号，新建设计源文件。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541240/39.png)

<span style="font-size:16px;">Create File。File name为myio_top。点击Finish。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541300/40.png)

<span style="font-size:16px;">点击OK，点击Yes。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541346/41.png)

<span style="font-size:16px;">要将main_dummy_top0替换成myio_top。在myio_top中例化ahb_axi_wrappper，并添加与原dummy模块文件中相同的端口。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541401/42.png)

<span style="font-size:16px;">相关RTL代码：</span><br>

	module myio_top(haddr, hclk, hprot, hrdata, hready, hresp, hrst_b, hsel, hsize, htrans, hwdata,  hwrite, hburst,//新增
	  intr,
	  myio//新增
	);
	output [31:0] myio;
	input   hburst;
	input   [31:0]  haddr;        
	input           hclk;         
	input   [3 :0]  hprot;        
	input           hrst_b;       
	input           hsel;         
	input   [2 :0]  hsize;        
	input   [1 :0]  htrans;       
	input   [31:0]  hwdata;       
	input           hwrite;       
	output  [31:0]  hrdata;       
	output          hready;  
	output  [1 :0]  hresp;    
	output                intr;    
	wire  [31:0]  hrdata;       
	wire          hready;  
	wire  [1 :0]  hresp;    
	wire          intr;
	wire [2:0] hburst;
	wire hready_in;
	assign hready_in = hready;
	wire [31:0] myio;    
	ahb_axi_wrapper u_ahb_axi_wrapper(//例化ahb_axi_wrapper模块
	   .AHB_INTERFACE_haddr      (haddr),
	   .AHB_INTERFACE_hburst     (hburst),
	   .AHB_INTERFACE_hprot      (hprot),
	   .AHB_INTERFACE_hrdata     (hrdata),
	   .AHB_INTERFACE_hready_in  (hready_in),
	   .AHB_INTERFACE_hready_out (hready),
	   .AHB_INTERFACE_hresp      (hresp),
	   .AHB_INTERFACE_hsize      (hsize),
	   .AHB_INTERFACE_htrans     (htrans),
	   .AHB_INTERFACE_hwdata     (hwdata),
	   .AHB_INTERFACE_hwrite     (hwrite),
	   .AHB_INTERFACE_sel        (hsel),
	   .myio                     (myio),
	   .s_ahb_hclk               (hclk),
	   .s_ahb_hresetn            (hrst_b)
	);
	endmodule

<span style="font-size:16px;">要将main_dummy_top0替换成myio_top。依次修改ahb_matrix_top，pdu_top，wujian100_open_top中的例化。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541624/43.png)

<span style="font-size:16px;">双击打开修改ahb_matrix_top文件</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541669/44.png)

<span style="font-size:16px;">找到x_main_dummy_top0的例化</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541716/45.png)

<span style="font-size:16px;">1.还要添加新增的output端口myio，信号需要引出到最顶层，myio</span><br>
<span style="font-size:16px;">2.新增了hburst,之前的dummy空模块中未使用，这里需要加上。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541787/46.png)

<span style="font-size:16px;">在改文件开始处，增加输出引脚和定义：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541832/47.png)

<span style="font-size:16px;">双击打开修改pdu_top文件：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541883/48.png)

<span style="font-size:16px;">找到例化的ahb_matrix_top，添加myio连接</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542183/49.png)

<span style="font-size:16px;">同样，增加输出引脚和定义</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542227/50.png)

<span style="font-size:16px;">双击打开修改wujian100_open_top文件</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542274/51.png)

<span style="font-size:16px;">找到例化的pdu_top，添加myio连接</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542322/52.png)

<span style="font-size:16px;">同样，增加输出引脚和定义</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542381/53.png)

<span style="font-size:16px;">现在就实现了IP的挂载。</span><br>
<span style="font-size:16px;">在约束文件中添加对应功能的引脚，这里将myio的低9位连接到三色灯的9个引脚上。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542436/54.png)

<span style="font-size:16px;">像之前的教程一样，综合，实现，再生成BIT文件，下载到开发板上。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542482/55.png)

### 3. 实现与验证
<span style="font-size:16px;">在CDK中编写简单的程序验证功能。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542543/56.png)
