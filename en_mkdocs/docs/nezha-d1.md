# D1 Chip Introduction
​ 【The Light of Domestic Semiconductors】【Allwinner Technology & Ali Pinto Joint Development】

​ 【RISC-V open source instruction set】【World's first chip with Pinto C906 core】

![](https://d1.docs.allwinnertech.com/assets/img/image-20210508170105959-1620464505246.png)

**D1 is Allwinner Technology's first chip based on RISC-V instruction set, integrated with Ali Pinto's 64-bit C906 core, supports RVV, 1GHz main frequency, and can support Linux, RTOS and other systems. It also supports up to 4K H.265/H.264 decoding, a built-in HiFi4 DSP and up to 2GB DDR3 external connection, which can be applied to various fields such as smart city, smart car, smart business display, smart home appliance, smart office and research and education.**

To facilitate developers' learning and partners' solution evaluation, Allwinner Online has customized a highly integrated dedicated development board based on the D1 chip, code name: Nezha!

For more information, please see:[D1 Development Board - Nezha](https://www.rvboards.org/mkdocs/zh/D1/ "D1 Development Board - Nezha")
## Block diagram
![](https://d1.docs.allwinnertech.com/assets/img/image-20210323105118258.png)
## Specifications
### CPU
```asp
Ali Pingtou Ge xuantie C906 main core, 64bit RISC-V instruction set
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

