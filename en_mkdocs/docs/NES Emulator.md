
![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1642062905/1.png)

<span style="font-size:16px;">
RVBoards D1 Nezha builds the QT environment through RVBoards OS, and runs the NES emulator (based on QT5) on the HDMI display.

The NES emulator can help you run NES games and let you feel the classics of the past again!

Connect the RVBoards D1 Nezha development board to the keyboard and you can play Contra directly.
You can play Contra through the "1 2 A W S D L O" keys.

Button usage instructions:

	1：choose    2：confirm/pause
	
	A：Left     W：On    S：Down    D：Right
	
	L：Attack    O：Jump
	

RVBoards OS preparation：

  1、	Install qt environment

   a)	apt install qtbase5-dev

  2、	Get the Qt source code of the nes simulator：qt4-nes4_5_512_480_640_480.7z

   a)	Link：[https://pan.baidu.com/s/1aoLBAk8u2e1vuywkj30P1g](https://pan.baidu.com/s/1aoLBAk8u2e1vuywkj30P1g "https://pan.baidu.com/s/1aoLBAk8u2e1vuywkj30P1g") Extraction code：4sif

   b)	WhyCan Forum Wow cool developer community, original link：[https://whycan.com/t_7253.html](https://whycan.com/t_7253.html "https://whycan.com/t_7253.html")

  3、	Compile the nes simulator

   a)	Unzip the source code of the nes simulator

     i.	7z x qt4-nes4_5_512_480_640_480.7z

   b)	Enter the source directory

     i.	cd qt4-NES4_5_512_480_640_480/Qt

   c)	Execute qmake to generate Makefile

     i.	qmake

   d)	Clear intermediate files

     i.	make clean

   e)	Compile and generate executable file Qt

     i.	make

     ii.	Compile error

       1.	ui_NesEmulateWindow.h:17:10: fatal error: nesscreenwidget.h: No such file or directory

         a)	ui_NesEmulateWindow.h This file is required for testing in the windows environment, just comment this sentence in the linux environment

   f)	Run the nes emulator and start the game

     i.	./Qt

   g)	Load Contra nes file hdl.nes

     i.	The nes simulator will load the nes file in the root directory by default 

     ii.	If there is no root directory, click "open" and select the location of the nes file

The source code of the NES simulator is taken from: WhyCan Forum Wow Cool Developer Community
（Original link：[https://whycan.com/t_7253.html](https://whycan.com/t_7253.html "https://whycan.com/t_7253.html") ）

</span>
