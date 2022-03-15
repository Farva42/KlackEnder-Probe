## KlackEnder Probe

KlackEnder Probe - **Simple, fast and cheap!**
  
Adaptation of the [Klicky](https://github.com/jlas1/Klicky-Probe)/[Quickdraw](https://github.com/Annex-Engineering/Quickdraw_Probe) Probe for the Ender 3 and comparable         Creality printers. The probe is compatible with all printers that use the X plate of the Ender 3. The cost of the probe is <5€, of which the switch is the most expensive part.
The probe is compatible with **Marlin and Klipper**. Both firmwares work with the G29 command, the docking is done automatically by the printer, it couldn't be easier! Both    firmwares add a KlackEnder menu to the display that can be used to dock and undock the Probe. The Bed-Mesh can be created via the custom menu, via the default formware settings or with G29.

### Quick Overwiew:
- Compatible with Marlin and Klipper. Firmware is provided.
- Automatic docking and undocking of the probe.
- Cuatom menu to control the probe.
- Cheap way to get fast and accurate probing.
- Easy to install, no soldering.
- work with all print surfaces

    Its working very well for me. If you have any questions ask me here or feel free to contact me on Discord: kevinakasam#2097 


   <img src="https://github.com/kevinakasam/KlackEnder-Probe/blob/main/Images/KlackEnder.gif" width="400" height="400" />

### BOM - Parts you need:
- 1x OMRON D2F or similar switch
- 4x Magnet 3x6mm 
- 2x M3x8mm screw (SHCS or BHCS doesn't matter)
- 3x M5x8mm screw (SHCS or BHCS doesn't matter)
- 3x M5 t-nut
- small cable tie and some cable (you may also need a connector to connect the probe to the mainboard e.g JST XH)


---

## Wiring Guide
Since there is no polarity on Swichtes, it doesn't matter which wire goes where. Just connect the switch to the two marked pins.
In the next chapter about firmware changes you will see where to add the pin.

**If you want me to add more mainboards feel free to contact me on Discord: kevinakasam#2097**

#### Stock Ender 3+Pro / Creality3D V1.1.x
- Currently I do not know how to connect an additional endstop to the stock Creality3D V1.1.x Mainboard
       
    <img src="https://i1.wp.com/www.th3dstudio.com/wp-content/uploads/2017/12/CR10v112.jpg?fit=1200%2C828&ssl=1" height="300" />

- Image source [3D-Druck-Community](https://www.3d-druck-community.de/showthread.php?tid=23449)
- Pin for Firmware: 

#### Ender 3 V2 / Silent Board V4.2.7 (or all Creality3D V4.x.x)
- Connect the probe to the two marked pins (G and Out). This pins would be also used to connect a BL-Touch.
       
    <img src="https://github.com/kevinakasam/KlackEnder-Probe/blob/main/Images/V4.2.7.jpg" height="300" />

- Image source [Creality3D](https://creality3d.shop/products/creality3d-upgrade-silent-4-2-7-1-1-5-mainboard-for-ender-3-ender-3-pro-ender-5-3d-printer?lang=de)
- Pin for Firmware: PB1

#### BIGTREETECH SKR Mini E3 V1.x
- Connect the probe to the two marked pins (Probe port).
       
    <img src="https://github.com/kevinakasam/KlackEnder-Probe/blob/main/Images/SKR-Mini-V1.x.jpg" height="300" />

- Image source [printertec](https://www.printertec.ch/elektronik/arduino/335/skr-mini-e3-v1.2-control-board-32-bit-cpu-32bit-board-fuer-ender-cr-10)
- Pin for Firmware: PC14

#### BIGTREETECH SKR Mini E3 V2.x
- Connect the probe to the two marked pins (Part of the BL-Touch port).
       
    <img src="https://github.com/kevinakasam/KlackEnder-Probe/blob/main/Images/SKR-Mini-V2.x.jpg" height="300" />

- Image source [BIGTREETECH](https://ae01.alicdn.com/kf/H27db29b02f354dc3abb6e36905bc45cdm/BIGTREETECH-BTT-SKR-MINI-E3-V2-Control-Board-32bit-Mit-TMC2209-3D-Drucker-Teile-Motherboard-F.jpg_Q90.jpg_.webp)
- Pin for Firmware: PC14

#### BIGTREETECH SKR Mini E3 V3.x
- Connect the probe to the two marked pins (Probe port).
       
    <img src="https://github.com/kevinakasam/KlackEnder-Probe/blob/main/Images/SKR-Mini-V3.x.jpg" height="300" />

- Image source [3djake](https://www.3djake.de/bigtreetech/skr-mini-e3)
- Pin for Firmware: PC14
