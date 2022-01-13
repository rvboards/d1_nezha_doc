<div style="width:100%;text-align:center;">
![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1642062905/1.png)
</div>

<span style="font-size:16px;">
RVBoards D1哪吒通过RVBoards OS搭建QT环境，并且在HDMI显示器上运行NES模拟器(基于QT5)。

NES模拟器可以帮助您运行NES游戏,让您再次感受往日经典!

RVBoards D1哪吒开发板接上键盘就可以直接玩魂斗罗。
通过“1 2 A W S D L O ”这几个键就可以玩魂斗罗啦。

按键使用说明：

	1：选择    2：确认/暂停
	
	A：左     W：上    S：下    D：右
	
	L：攻击    O：跳
	

RVBoards OS准备工作：

  1、	安装qt环境

   a)	apt install qtbase5-dev

  2、	获取nes模拟器Qt源码：qt4-nes4_5_512_480_640_480.7z

   a)	链接：[https://pan.baidu.com/s/1aoLBAk8u2e1vuywkj30P1g](https://pan.baidu.com/s/1aoLBAk8u2e1vuywkj30P1g "https://pan.baidu.com/s/1aoLBAk8u2e1vuywkj30P1g") 提取码：4sif

   b)	WhyCan Forum 哇酷开发者社区，原文链接：[https://whycan.com/t_7253.html](https://whycan.com/t_7253.html "https://whycan.com/t_7253.html")

  3、	编译nes模拟器

   a)	解压nes模拟器源码

     i.	7z x qt4-nes4_5_512_480_640_480.7z

   b)	进入源码目录

     i.	cd qt4-NES4_5_512_480_640_480/Qt

   c)	执行qmake，生成Makefile

     i.	qmake

   d)	清除中间文件

     i.	make clean

   e)	编译生成执行文件Qt

     i.	make

     ii.	编译出错

       1.	ui_NesEmulateWindow.h:17:10: fatal error: nesscreenwidget.h: No such file or directory

         a)	ui_NesEmulateWindow.h在windows环境中测试需要此文件，linux环境中注释此句即可

   f)	运行nes模拟器，开始游戏

     i.	./Qt

   g)	加载魂斗罗nes文件hdl.nes

     i.	nes模拟器会默认加载根目录下的nes文件 

     ii.	如果根目录下没有，单击“open”，选择nes文件所在位置

NES模拟器源码取自：WhyCan Forum 哇酷开发者社区
（原文链接：[https://whycan.com/t_7253.html](https://whycan.com/t_7253.html "https://whycan.com/t_7253.html") ）

</span>

