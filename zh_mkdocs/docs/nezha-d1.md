# D1 芯片介绍
​ 【国产半导体之光】 【全志科技&阿里平头哥 联合开发】

​ 【RISC-V开源指令集】【全球首款平头哥C906核心的芯片】
![](https://d1.docs.allwinnertech.com/assets/img/image-20210508170105959-1620464505246.png)

**D1 是全志科技首款基于RISC-V指令集的芯片，集成了阿里平头哥64位C906核心，支持RVV，1GHz主频，可支持Linux、RTOS等系统。同时支持最高4K的H.265/H.264解码，内置一颗HiFi4 DSP，最高可外接2GB DDR3，可以应用于智慧城市、智能汽车、智能商显、智能家电、智能办公和科研教育等多个领域。**

为方便开发者学习和合作伙伴进行方案评估，全志在线基于D1芯片定制了高集成度专用开发板，代号：哪吒！

详情请见：[D1开发板-哪吒](https://www.rvboards.org/mkdocs/zh/D1/ "D1开发板-哪吒")
## 芯片框图
![](https://d1.docs.allwinnertech.com/assets/img/image-20210323105118258.png)
## 参数规格
### CPU
```asp
阿里平头哥玄铁C906主核，64bit RISC-V指令集
32 KB I-cache + 32 KB D-cache
```
### DSP
```asp
HiFi4 DSP  600MHz

32 KB I-cache + 32 KB D-cache

64 KB I-ram + 64 KB D-ram
```
### Memory
```
DDR2/DDR3, up to 2 GB

SD3.0/eMMC 5.0, SPI Nor/Nand Flash
```
### Video Engine
```
Video decoding

    - H.265 up to 1080p@60fps, or 4K@30fps

    - H.264 up to 1080p@60fps, or 4K@24fps

    - MPEG-1/2/4, JPEG, VC1 up to 1080p@60fps

Video encoding

    - JPEG/MJPEG up to 1080p@60fps

    - Supports input picture scaler up/down
```
### Video OUT
```
RGB LCD output interface up to 1920 x 1080@60fps

Dual link LVDS interface up to 1920 x 1080@60fps

4-lane MIPI DSI interface up to 1920 x 1080@60fps

HDMI V1.4 output interface up to 4K@30fps

CVBS OUT interface, supporting NTSC and PAL format
```
### Video IN
```
8-bit parallel CSI interface

CVBS IN interface, supporting NTSC and PAL format
```
### Audio

```
2 DACs and 3 ADCs

Analog audio interfaces: MICIN1P/N, MICIN2P/N, MICIN3P/N, FMINL/R, LINEINL/R, LINEOUTLP/N, LINEOUTRP/N, HPOUTL/R

Digital audio interfaces: I2S/PCM, DMIC, OWA IN/OUT
```
### Connectivity
```
USB2.0 OTG, USB2.0 Host

SDIO 3.0, SPI x 2, UART x 6, TWI x 4

PWM (8-ch), GPADC (2-ch), LRADC (1-ch), TPADC (4-ch), IR TX&RX

10/100/1000M EMAC with RMII and RGMII interfaces
```
### Package
```
LFBGA BGA13*13/0.35/0.65mm,337 PINS
Chip process

22nm
```
微信官宣发布链接：https://mp.weixin.qq.com/s/Sv8ownFF2d-sKjBDMXp-bQ
