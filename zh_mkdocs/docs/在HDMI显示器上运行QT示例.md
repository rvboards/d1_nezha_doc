
![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1642065563/1.png)


<span style="font-size:16px;">
RVBoards D1哪吒通过RVBoards OS搭建QT环境，并且在HDMI显示器上运行QT示例。

示例简介

QT 生成10000个随机数，利用QT thread库创建两个线程，一个采用快速排序，一个采用冒泡排序，对比两种排序算法的性能，输出排序所用时间。

RVBoards OS准备工作：

  1、	安装qt环境

      a)	apt install qtbase5-dev

  2、	获取QT示例源码：QThread_sort_demo.tar.gz

      a)	链接：https://pan.baidu.com/s/1aoLBAk8u2e1vuywkj30P1g 提取码：4sif

  3、	编译示例

      a)	解压QT示例源码

          i.	tar –zxf QThread_sort_demo.tar.gz

      b)	进入源码目录

          i.	cd QThread_sort_demo

      c)	执行qmake，生成Makefile

          i.	Qmake

      d)	清除中间文件，编译生成执行文件Qtread_01

          i.	make clean && make

      e)	运行Qtread_01，点击开始，查看结果

          i.	./Qthread_01

</span>
