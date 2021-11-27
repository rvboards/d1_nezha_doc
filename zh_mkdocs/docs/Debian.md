### 版本更新介绍

<span style="font-size:16px;">

版本更新相关信息请参考：

[https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95](https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95 "https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95")

</span>

### 烧录方法

#### 基本介绍

<span style="font-size:16px;">

本文档介绍在RVBoards-D1-哪吒开发板启动Debian系统。

包含RVBoards_D1_debian_min.img和RVBoards_D1_debian_desktop.img文件。

		username: root
		password: rvboards

</span>

#### 需要的系统环境

<span style="font-size:16px;">

Windows（推荐win10）；

</span>

#### 需要的相关工具

<span style="font-size:16px;">

软件部分：PhoenixCard

硬件部分：SD卡，推荐使用32GB

</span>

#### 需要的镜像文件

<span style="font-size:16px;">

RVBoards_D1_debian_min.img 仅仅是一个基本的Debian镜像文件

RVBoards_D1_debian_desktop.img 包含图形界面的Debian镜像文件

</span>

#### PhoenixCard软件安装（需要环境windows）

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1630461529/1.png)

#### 烧录kernel镜像

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1630461610/2.png)

#### 启动RVBoards-D1-哪吒

<span style="font-size:16px;">

插入SD卡，通电；

如果烧录RVBoards_D1_debian_min.img镜像文件，需要连接串口；

如果烧录RVBoards_D1_debian_desktop.img镜像文件，插入HDMI接口，开机进入Debian桌面。

注意事项：执行 apt-get **相关命令前需要更新系统时间；

命令（例）：

		date -s “20210512 19:59:00”

</span>

### 镜像软件源配置

![](https://rvboards.org/rvboards/dasdu8syrbgvtzvhfj12f4d5/images_dir/1630461840/3.png)

### 相关的问题

<span style="font-size:16px;">

相关问题请参考链接：

[https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95](https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95 "https://www.rvboards.org/forum/cn/topic/61/rvboards-%E5%93%AA%E5%90%92-d1-debian%E7%B3%BB%E7%BB%9F%E9%95%9C%E5%83%8F%E5%92%8C%E5%AE%89%E8%A3%85%E6%96%B9%E6%B3%95")

</span>

