## 实验目的
<span style="font-size:16px;">主要完成wujian100 SoC在FPGA上的部署。学会使用Xilinx vivado工具。</span><br>

## 实验步骤
### 1. 把wujian100用Vivado打开

<span style="font-size:16px;">1) 创建工程</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955380/25.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955423/26.png)

<span style="font-size:16px;">next后添加 verilog 源码：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955469/27.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955501/28.png)

<span style="font-size:16px;">点击next后添加xdc文件</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955565/29.png)

<span style="font-size:16px;">选择开发板</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955610/30.png)

<span style="font-size:16px;">2) 文件添加进来后，VIVADO 会自动识别、编译、分析，VIVADO 分析文件中的错误，用红色波浪线标识（错误原因是没有识别出头文件，将这四个文件类型改为头文件类型即可）</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955669/31.png)

<span style="font-size:16px;">3) 调用时钟IP</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955725/32.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955761/33.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955799/34.png)

### 2. 根据 perfv 开发板手册添加管脚约束
<span style="font-size:16px;">详细见文件“xdc的更改”.</span><br>

### 3. 综合工程，综合无误后进行bit流下载

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955904/35.png)

<span style="font-size:16px;">可能出现error-某某module未找到，注释掉这个module就行</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955947/36.png)

<span style="font-size:16px;">综合结果如下：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657955993/37.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956075/38.png)

### 4. 下载到开发板上
<span style="font-size:16px;">1) 接口连接电脑和开发板</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956148/39.png)

<span style="font-size:16px;">2) 固化FLASH</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956198/40.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956230/41.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956264/42.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956292/43.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1657956322/44.png)

<span style="font-size:16px;">显示5表明wujian100已经下载到了开发板里，并且上电复位就可以运行。</span><br>
