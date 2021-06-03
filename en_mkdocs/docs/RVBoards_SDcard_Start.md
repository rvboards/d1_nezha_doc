# Basic introduction

This document describes launching the Debian system on the RVBoards-D1-nezha development board.

include RVBoards_D1_Debian_lxde_img_win_v0.4.zip and RVBoards_D1_Debian_lxde_img_linux_v0.4.gz file，They can be burned in Linux and Windows environments, respectively.

```
username: root
password:rvboards
```
## Part 1:Windows

### Required system environment

Windows（recommended win10）；

### Relevant tools required

Required software：PhoenixCard;
Required hardware：SD卡，32GB is recommended;

### Required img file

RVBoards_D1_Debian_lxde_img_win_v0.4.zip

### PhoenixCard software installing 

Click PhoenixCard.exe to install the burning software;

### Burn Img file

![burning](G:\micro_programing\D1\img\burning.png)

It takes about 15 minutes;

<img src="G:\micro_programing\D1\img\burning_ok.png" alt="burning_ok" style="zoom:80%;" />

## Part 2：Linux

### Required system environment

LInux (Ubuntu or Debian);

### Relevant tools required

Required software：PhoenixCard;
Required hardware：SD卡，32GB is recommended;

### Required img file

RVBoards_D1_Debian_lxde_img_linux_v0.4.gz

### Burn Img file

```
sudo gzip -dc RVBoards_D1_Debian_lxde_img_linux_v0.4.gz | sudo dd of=/dev/sdc
```

## Start RVBoards-D1-nezhe

### Step 1：

connect the cable to the display at the HDMI port

### step 2:

connect a mouse and Keyboard to the USB HOST interface

### step 3:

connect the power supply cable to the POWER connector 

log in after the login interface pops up

## Download :

https://www.rvboards.org/forum/en/topic/4/rvboards-allwinner-d1-debian-os-images/2

## Technical support

RVBoards BBS [Home | RVBoards Forum](https://www.rvboards.org/forum/en/)



