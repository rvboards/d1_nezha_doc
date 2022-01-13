<div style="width:100%;text-align:center;">
![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1642065563/1.png)
</div>

<span style="font-size:16px;">
RVBoards D1 Nezha builds the QT environment through RVBoards OS, and runs the QT example on the HDMI display.

Sample introduction

QT generates 10,000 random numbers, uses the QT thread library to create two threads, one uses quick sort and the other uses bubble sort, compares the performance of the two sorting algorithms, and outputs the time used for sorting.

RVBoards OS preparation:

  1、	Install qt environment

      a)	apt install qtbase5-dev

  2、	Get the QT sample source code：QThread_sort_demo.tar.gz

      a)	Link：https://pan.baidu.com/s/1aoLBAk8u2e1vuywkj30P1g Extraction code：4sif

  3、	Compile the example

      a)	Unzip the QT example source code

          i.	tar –zxf QThread_sort_demo.tar.gz

      b)	Enter the source directory

          i.	cd QThread_sort_demo

      c)	Execute qmake to generate Makefile

          i.	Qmake

      d)	Clear the intermediate files, compile and generate the executable file Qtread_01

          i.	make clean && make

      e)	Run Qtread_01, click Start to see the results

          i.	./Qthread_01

</span>
