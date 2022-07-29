## Experimental goal
<span style="font-size:16px;">There are many dummy modules in Wujian100, which can be customized by users. This document uses the Dummy0 module on the AHB bus to control the RGB LED peripheral by writing registers.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539100/1.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539132/2.png)

<span style="font-size:16px;">This experiment builds its IP in vivado, and the IP is the AXI4 interface. The control based on the three-color LED light requires 9 bits, and here the lower 9 bits of the 32-bit register 0 are used as the control output. Mount IP to wujian100, and implement and verify functions.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539182/3.png)

## Experimental steps
### 1. Create Block Design
<span style="font-size:16px;">Wujian100 soft core is AHB bus, VIVADO supports AXI bus IP, need to use AHB-Lite to AXI Bridge adapter module.</span><br>
<span style="font-size:16px;">Click Create Block Design, enter the design name, and open the Block Design interface.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539305/4.png)

<span style="font-size:16px;">Click the plus sign to add IP, search for AHB-Lite to AXI Bridge, and double-click to add.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539359/5.png)

<span style="font-size:16px;">Click on the module, press the icon or Ctrl+T to export the port. The bridge module acts as the AXI master, and the custom IP is the AXI slave.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539419/6.png)

<span style="font-size:16px;">The port name in the source file needs to be modified later, the suffix will be removed here, it will be more convenient when editing later</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539506/7.png)

<span style="font-size:16px;">Create your AXI IP core and customize your AXI IP. Click Tools->Create and Package New IP.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539580/8.png)

<span style="font-size:16px;">Click Next.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539633/9.png)

<span style="font-size:16px;">Select the IP to create the AXI peripheral and click Next.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539683/10.png)

<span style="font-size:16px;">You can name the IP yourself and write a description.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539734/11.png)

<span style="font-size:16px;">The bridge is the master, and we create the slave mode. As shown below, click Next.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539786/12.png)

<span style="font-size:16px;">Click the IP Catalog on the left, open the IP manager, see the myio just added → right-click myio_v1.0 → Edit in IP Packager option, click OK, then the system will automatically open another Vivado IDE to perform the user IP core.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539834/13.png)

<span style="font-size:16px;">In this module, 4 registers are set, and each register is 32 bits wide. Here, by writing data to the register, the level of the output port is controlled, thereby controlling the output of the tricolor lamp. Connect the output port to the register register.</span><br>
<span style="font-size:16px;">Double click to enter myio_v1_0_S00_AXI, there is a user code area in the design file.</span><br>
<span style="font-size:16px;">Increase port declarations and add user signals as needed. Here an output [31:0]myio is added to control the three-color light.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539917/14.png)

<span style="font-size:16px;">Add user logic code as required. Here, add assign myio = slv_reg0; to connect the output to register 0.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658539971/15.png)

<span style="font-size:16px;">Double click to enter the top layer of IP, increase output [31:0]myio</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540029/16.png)

<span style="font-size:16px;">Add .myio(myio) to the instantiation,</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540076/17.png)

<span style="font-size:16px;">Changes will be refreshed. Switch to the Package IP-myio window, click the link shown in the figure, and update the top-level file that was just modified.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540130/18.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540166/19.png)

<span style="font-size:16px;">Repackage the IP</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540225/20.png)

<span style="font-size:16px;">Now that the IP can be used, add the IP to the Block Design.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540284/21.png)

<span style="font-size:16px;">But their AXI ports are still a little different, they can't be connected, and an interconnected IP needs to be added.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540340/22.png)

<span style="font-size:16px;">Add AXI Interconnect module</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540388/23.png)

<span style="font-size:16px;">Double-click to open the AXI Interconnect module, and the interfaces of Slave and Master are both 1.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540439/24.png)

<span style="font-size:16px;">You can drag and drop with the mouse to connect ports</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540498/25.png)

<span style="font-size:16px;">Just click to connect automatically</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540543/26.png)

<span style="font-size:16px;">Automatically connect so, click OK.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540589/27.png)

<span style="font-size:16px;">After the automatic wiring, a new module appears to connect the rst signal, delete it here and connect it manually.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540644/28.png)

<span style="font-size:16px;">Connect the reset signal manually.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540699/29.png)

<span style="font-size:16px;">Select the myio module, ctrl+t leads to the output</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540765/30.png)

<span style="font-size:16px;">Change the name as before, to myio</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540811/31.png)

<span style="font-size:16px;">assign address. Go to the Adress Editor interface, find myio_0, and right-click on Assign.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540858/32.png)

<span style="font-size:16px;">Modify the address to the first address of dummy0, 0x4001_0000.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540925/33.png)

<span style="font-size:16px;">Go back to the diagram window, click to verify, that there is no error, and exit block design.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658540978/34.png)

### 2. Connect IP to wujian100
<span style="font-size:16px;">Wrapper that generates IP. Find the generated ahb_axi in Source, right-click Generate Output Products</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541046/35.png)

<span style="font-size:16px;">Then right-click Create HDL Wrapper.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541090/36.png)

<span style="font-size:16px;">Click OK。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541131/37.png)

<span style="font-size:16px;">You can see that the wrapper is generated and can be called, or an additional layer of files can be called.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541194/38.png)

<span style="font-size:16px;">Add a top-level file to your design. Click the + sign to create a new design source file.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541240/39.png)

<span style="font-size:16px;">Create File. File name is myio_top. Click Finish.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541300/40.png)

<span style="font-size:16px;">Click OK, click Yes.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541346/41.png)

<span style="font-size:16px;">Replace main_dummy_top0 with myio_top. Instantiate ahb_axi_wrappper in myio_top and add the same port as in the original dummy module file.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541401/42.png)

<span style="font-size:16px;">Relevant RTL code:</span><br>

	module myio_top(haddr, hclk, hprot, hrdata, hready, hresp, hrst_b, hsel, hsize, htrans, hwdata,  hwrite, hburst,//new
	  intr,
	  myio//new
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
	ahb_axi_wrapper u_ahb_axi_wrapper(//Instantiate the ahb_axi_wrapper module
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

<span style="font-size:16px;">Replace main_dummy_top0 with myio_top. Modify the instantiations in ahb_matrix_top, pdu_top, wujian100_open_top in turn.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541624/43.png)

<span style="font-size:16px;">Double-click to open the modified ahb_matrix_top file</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541669/44.png)

<span style="font-size:16px;">Find the instantiation of x_main_dummy_top0</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541716/45.png)

<span style="font-size:16px;">1. Also add the new output port myio, the signal needs to be led out to the top level, myio</span><br>
<span style="font-size:16px;">2. Added hburst, which was not used in the previous dummy empty module, and needs to be added here.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541787/46.png)

<span style="font-size:16px;">At the beginning of the file, add output pins and definitions:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541832/47.png)

<span style="font-size:16px;">Double-click to open the modified pdu_top file:</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658541883/48.png)

<span style="font-size:16px;">Find the instantiated ahb_matrix_top and add myio connection</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542183/49.png)

<span style="font-size:16px;">Again, add output pins and define</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542227/50.png)

<span style="font-size:16px;">Double-click to open the modified wujian100_open_top file</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542274/51.png)

<span style="font-size:16px;">Find the instantiated pdu_top and add the myio connection</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542322/52.png)

<span style="font-size:16px;">Again, add output pins and define</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542381/53.png)

<span style="font-size:16px;">The IP is now mounted.</span><br>
<span style="font-size:16px;">Add the corresponding function pins in the constraint file, where the lower 9 bits of myio are connected to the 9 pins of the tricolor lamp.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542436/54.png)

<span style="font-size:16px;">As in the previous tutorial, synthesize, implement, and then generate a BIT file and download it to the development board.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542482/55.png)

### 3. Implementation and verification
<span style="font-size:16px;">Write simple program verification functions in CDK.</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658542543/56.png)
