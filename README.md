# MeshCalc
Meshtastic running on Clockwork PicoCalc (Powered by Luckfox Lyra running on Ubuntu OS)

BOARD | Tested OK |
|:--|:--|
| Keybaord | Yes |
| Virtual Mouse via keyboard | Yes |
| Display | Yes | 
| USB port | Yes |
| SPI LoRa wio-sx1262 | Yes |
| USB Networking | Yes |
| ADB | Yes |
| SDCARD Slot | No - remapped the spi bus to the external pins instead |
| Audio | No - needs hw mod and another gpio as i used it for LoRa |
| USB WiFi | No - but maybe could look at incl some |

https://www.clockworkpi.com/

https://forum.clockworkpi.com/t/luckfox-lyra-on-picocalc/16280

# ** Wip **

# ** [Connection - External GPIO Used] **
![image](https://github.com/user-attachments/assets/efe95224-e7ff-4623-b3cd-f3e74317f6af)

```
Pinout (pictured above)

Core GPIOs  LoRa OK  

1 3V3 Output   3V3 | 3V3   Red  
2 GP2  RAM_TX    RM_IO12   MOSI   Blue  
3 GP3  RAM_RX    RM_IO13   MISO   Green  
4 GP4  RAM_IO2   RM_IO0   [Rxen]   Gray  
5 GP5  RAM_IO3	  RM_IO1 | IRQ   Purple  
6 GP21 RAM_SCK	  RM_IO26   SCK   Yellow  
7 GP28 Free   RM_IO24   CS   Orange  
8 GND   GND   GND   Black 

Mainboard GPIOs
1 3V3 OUT               3V3             3V3             Red
2 GP0 	UART0_TX	RM_IO22		Busy		Brown
3 GP1 	UART0_RX	RM_IO23		Reset		White
4 UART1_RX		NC		NC                              CKS32F103Rx
5 UART1_TX		NC		NC                              CKS32F103Rx
6 USB_DP                NC              NC
7 USB_DN                NC              NC
8 GND                   NC              NC
```

```
root@luckfox:/# gpioinfo 0
gpiochip0 - 32 lines:
        line   0:      unnamed  "portduino"  output  active-high [used]
        line   1:      unnamed  "portduino"   input  active-high [used]
        line   2:      unnamed "ili9488_drv" output active-high [used]
        line   3:      unnamed "ili9488_drv" output active-high [used]
        line   4:      unnamed "ili9488_drv" output active-high [used]
        line   5:      unnamed       unused   input  active-high 
        line   6:      unnamed       unused   input  active-high 
        line   7:      unnamed       unused   input  active-high 
        line   8:      unnamed       unused   input  active-high 
        line   9:      unnamed  "portduino"  output  active-high [used]
        line  10:      unnamed       unused   input  active-high 
        line  11:      unnamed       unused   input  active-high 
        line  12:      unnamed       unused   input  active-high 
        line  13:      unnamed       unused   input  active-high 
        line  14:      unnamed       unused   input  active-high 
        line  15:      unnamed       unused   input  active-high 
        line  16:      unnamed       unused   input  active-high 
        line  17:      unnamed       unused   input  active-high 
        line  18:      unnamed       unused   input  active-high 
        line  19:      unnamed       unused   input  active-high 
        line  20:      unnamed       unused   input  active-high 
        line  21:      unnamed       unused   input  active-high 
        line  22:      unnamed  "portduino"  output  active-high [used]
        line  23:      unnamed  "portduino"   input  active-high [used]
        line  24:      unnamed       unused   input  active-high 
        line  25:      unnamed       unused   input  active-high 
        line  26:      unnamed       unused   input  active-high 
        line  27:      unnamed       unused   input  active-high 
        line  28:      unnamed       unused   input  active-high 
        line  29:      unnamed       unused   input  active-high 
        line  30:      unnamed       unused   input  active-high 
        line  31:      unnamed       unused   input  active-high 
root@luckfox:/# 
```

![image](https://github.com/user-attachments/assets/0f3469a7-efee-4cfe-baec-044a8dada9b9)

# ** [Meshtastic User Interface running (Framebuffer Mode)] - you can use the keyboards virtual mouse option with arrow keys and brackets **
Press Right Shift to enable virtual mouse
![image](https://github.com/user-attachments/assets/d59cb872-b578-4668-80f1-e0a564466f18)

# Boot Image Required for Meshtatic

[Ubuntu 22.04]
Flash my other Ubuntu OS image for PicoCalc and then replace only boot.img
https://github.com/markbirss/ubuntu_22.04.5_lts_picocalc

Download Link

https://drive.google.com/drive/folders/1v10ZoPi9GQchSC77REZS3_fdjDz7eGtV?usp=sharing

or

[Ubuntu 24.04]

https://github.com/markbirss/ubuntu-24.04.2-meshtastic-picocalc-wio-sx1262

or 

[Ubuntu 24.04] Developer Image

https://github.com/markbirss/ubuntu-24.04.2-picocalc

Follow the meshtastic installation instructions from
https://meshtastic.org/docs/software/linux/installation/
```
# Install requirements for add-apt-repository
sudo apt install software-properties-common
# Add Meshtastic repo
sudo add-apt-repository ppa:meshtastic/alpha
# Install meshtasticd
sudo apt install meshtasticd
```

edit /etc/meshtasticd/config.yaml

you need to specify a MAC address / MAC sources for your nodes unique ID

Replace boot image (with your Luckfox Lyra connected to via USB)
```
7z x boot.z
sha256sum boot.img

538b74d6b02b428a3506122c36815fa4cc0b6929808240d505f0635fc0c4d2dc  boot.img

adb reboot loader
sudo ./upgrade_tool td
sudo ./upgrade_tool di -b ./boot.img
sudo ./upgrade_tool rd

```

Meshtastic LoRa config.yaml

/etc/meshtasticd/config.d/lora-lyra-picocalc-wio-sx1262.yaml
```
Lora:
  Module: sx1262
  DIO2_AS_RF_SWITCH: true
  DIO3_TCXO_VOLTAGE: true
  gpiochip: 0
  MOSI: 12
  MISO: 13
  IRQ: 1
  Busy: 23
  Reset: 22
  RXen: 0
  gpiochip: 1
  CS: 9
  SCK: 11
#  TXen: bridge to DIO2 on E22 module
  SX126X_MAX_POWER: 22
  spidev: spidev1.0
  spiSpeed: 2000000

```
# NOTE: the yaml file is whitespace sentsitive, keep the spaces

If you are using another SX1262 module simply comment out the RXen line with a #


Support my work and considder **buying  me a coffee**

https://buymeacoffee.com/mark.birss


