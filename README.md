# MeshCalc
Meshtastic running on Clockwork PicoCalc (Powered by Luckfox Lyra running on Ubuntu OS)

BOARD | Tested OK |
|:--|:--|
| Keybaord | Yes |
| Display | Yes | 
| USB port | Yes |
| SPI LoRa wio-sx1262 | Yes |
| USB Networking | Yes |
| ADB | Still todo |
| Audio | No - needs hw mod |


https://www.clockworkpi.com/

https://forum.clockworkpi.com/t/luckfox-lyra-on-picocalc/16280

# ** Wip **

# ** [Connection - External GPIO Used] **
![image](https://github.com/user-attachments/assets/efe95224-e7ff-4623-b3cd-f3e74317f6af)

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

# ** [Meshtastic User Interface running (Framebuffer Mode)] - needs a mouse as input device since display has no touch **
![image](https://github.com/user-attachments/assets/d59cb872-b578-4668-80f1-e0a564466f18)



Support my work and considder **buying  me a coffee**

https://buymeacoffee.com/mark.birss


