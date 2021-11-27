### Version update introduction

<span style="font-size:16px;">

For information about version updates, please refer to：

[https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95](https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95 "https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95")

</span>

### Burning method

#### Overview

<span style="font-size:16px;">

This document describes booting the Debian system on the RVBoards-D1-Nezha development board.

The files RVBoards_D1_debian_min.img and RVBoards_D1_debian_desktop.img are included.

		username: root
		password: rvboards

</span>

#### Required System Environment

<span style="font-size:16px;">

Windows（recommend win10）；

</span>

#### Required Related Tools

<span style="font-size:16px;">

Software：PhoenixCard

Hardware：SD card, recommend 32GB

</span>

#### Required Image Files

<span style="font-size:16px;">

RVBoards_D1_debian_min.img Just a basic Debian image file

RVBoards_D1_debian_desktop.img Debian image file with GUI included

</span>

#### PhoenixCard software installation (requires windows environment)

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1630461529/1.png)

#### Burning the kernel image

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1630461610/2.png)

#### Start RVBoards-D1-Nezha

<span style="font-size:16px;">

inserting the SD card and powering up

if burning the RVBoards_D1_debian_min.img image file, need to connect the serial port.

If burning RVBoards_D1_debian_desktop.img image file, insert HDMI port and power on into Debian desktop.

Caution: you need to update the system time before executing apt-get **related commands.

Command (example)：

		date -s “20210512 19:59:00”

</span>

### Mirroring software source configuration

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1630461840/3.png)

### Related Questions

<span style="font-size:16px;">

For related questions, please refer to the link：

[https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95](https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95 "https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95")

</span>




