## 实验目标
<span style="font-size:16px;">（1）在wujian100 SoC在FPGA上完成部署之后，通过设置该SoC的I/O引脚为高电平或者低电平，观察LED的亮灭，学会使用E902的I/O。</span><br>
<span style="font-size:16px;">（2）学会使用E902处理器读写SD卡，需要SD卡和SD卡的拓展板。</span><br>
<span style="font-size:16px;">注意：SD卡相关功能需要Pref的SD卡拓展板，借插口如下。SD卡的程序和LED的程序是一起的，所以一起就可以测试。</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193358/1.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193395/2.png)

## 实验步骤
### 1. 连接电脑和wujian100
<span style="font-size:16px;">Clink与PMOD连接：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193460/3.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193503/5.png)

<span style="font-size:16px;">如下对应关系：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193549/6.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193583/7.png)

### 2. 连接USB转串口下载器和开发

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193634/8.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193675/9.png)

### 3. 编译调试

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193722/10.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193751/11.png)

<span style="font-size:16px;">显示出来了E902才可以进行下一步，没有显示出来可以去查一下PMOD和CLINK的连接是不是错的，或者没连上。</span><br>

### 4. CDK的串口窗口

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193808/12.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193846/13.png)

### 5. 下载程序

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193889/14.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193919/15.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193950/16.png)

<span style="font-size:16px;">或者用这两个：</span><br>

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658193992/17.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658194029/18.png)

### 6. 复位后就会正确现象是灯闪烁，以及

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658194073/19.png)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1658194100/20.png)

<span style="font-size:16px;">表明SD卡读取正确，可以在Debug调试界面查看寄存器中具体的值。</span><br>
