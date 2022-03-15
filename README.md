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
- Works with all print surfaces

    Its working very well for me. If you have any questions ask me here or feel free to contact me on Discord: kevinakasam#2097 

<table>
  <tr>
    <td><img src="https://github.com/kevinakasam/KlackEnder-Probe/blob/main/Images/KlackEnder.gif" height="350"> </td>
    <td><img src="https://github.com/kevinakasam/KlackEnder-Probe/blob/main/Images/Image.png" height="350"> </td>
  </tr>
</table>

### BOM - Parts you need:
- 1x OMRON D2F or similar switch
- 4x Magnet 3x6mm 
- 2x M3x8mm screw (SHCS or BHCS doesn't matter)
- 3x M5x8mm screw (SHCS or BHCS doesn't matter)
- 3x M5 t-nut
- small cable tie and some cable (you may also need a connector to connect the probe to the mainboard e.g JST XH)


## Assembly Guide
I made a short video about the assembly and installation of the probe.

Wiring and firmware changes are described at the bottom of the page.

[![Video Guide](https://github.com/kevinakasam/KlackEnder-Probe/blob/main/Images/Preview.jpg)](https://youtu.be/2e0tamL57Yo "Click to Watch!")

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

## Firmware Guide
The KlackEnder probe works with Marlin and Klipper. This guide only shows you what changes you need to make to the firmware, not how to modify/upload the firmware itself. There are several guides online for different boards and printers.
**You do not have to use the ```Probe In``` or ```Probe Out``` macros.** They're just a nice to have. The printer will do this automatically when you send a ```G29```.

### Klipper

The installation for Klipper is pretty easy. Simply copy the code from the ```KlackEnder.cfg```to your ```printer.cfg```
The ```[gcode_macro G29]``` does the same like the ```[gcode_macro AUTO_BED_MESH]```. I just added this so you can use the G29 commend as usual.

Dont forgot to edit your probe Pin:
  ```
  #####################################################################
  #	KlackEnder- Settings
  #####################################################################

  [probe]
  pin: ^PC14 #Probe-Stop Connection on Skr Mini E3 DIP. Change this if needed!
  #z_offset: 0 #Measure per your specific setup
  x_offset: 8 # negative = left of the nozzle
  y_offset: 21 # negative = in front of of the nozzle
  speed: 5.0
  lift_speed: 15.0
  sample_retract_dist: 1
  samples: 2
  samples_tolerance_retries: 6

  ##[(7x7)-1] / 2 = 24
  ##[(5x5)-1] / 2 = 12
  [bed_mesh]
  speed: 300
  horizontal_move_z: 2
  mesh_min: 8,30
  mesh_max: 223,201
  probe_count: 5,5
  relative_reference_index: 12
  algorithm: bicubic
  fade_start: 1
  fade_end: 10
  #fade_target:
  #   The z position in which fade should converge. When this value is set
  #   to a non-zero value it must be within the range of z-values in the mesh.
  #   Users that wish to converge to the z homing position should set this to 0.
  #   Default is the average z value of the mesh.
  split_delta_z: 0.015
  #   The amount of Z difference (in mm) along a move that will
  #   trigger a split. Default is .025.
  move_check_distance: 3
  #   The distance (in mm) along a move to check for split_delta_z.
  #   This is also the minimum length that a move can be split. Default
  #   is 5.0.
  mesh_pps: 4,4
  #   A comma separated pair of integers (X,Y) defining the number of
  #   points per segment to interpolate in the mesh along each axis. A
  #   "segment" can be defined as the space between each probed
  #   point. The user may enter a single value which will be applied
  #   to both axes.  Default is 2,2.
  #bicubic_tension: .2
  #   When using the bicubic algorithm the tension parameter above
  #   may be applied to change the amount of slope interpolated.
  #   Larger numbers will increase the amount of slope, which
  #   results in more curvature in the mesh. Default is .2.

  #####################################################################
  #	KlackEnder- Macros
  #####################################################################

  [gcode_macro PROBE_OUT]
  gcode:
      G90
      G1 Z5
      G1 X245 F20000
      G1 Z0
      G4 P300
      G1 Z20
      G1 X0

  [gcode_macro PROBE_IN]
  gcode:
      G90
      G1 Z20
      G1 X245 F20000
      G1 Z0
      G4 P300
      G1 X240 F1000
      G1 Z5
      G4 P300
      G1 X0 F20000
      G1 Z0

  [gcode_macro AUTO_BED_MESH]
  gcode:
      PROBE_OUT
      BED_MESH_CALIBRATE
      G1 Y0 F20000
      PROBE_IN

  [gcode_macro G29]
  gcode:
      PROBE_OUT
      BED_MESH_CALIBRATE
      G1 Y0 F20000
      PROBE_IN

  #####################################################################
  #	KlackEnder- Menu
  #####################################################################

  [menu __main]
  type: list
  name: Main

  [menu __main __KlackEnder]
  type: list
  enable: True
  name: KlackEnder

  [menu __main __KlackEnder __ProbeOut]
  type: command
  name: Probe Out
  gcode:
      PROBE_OUT

  [menu __main __KlackEnder __ProbeIn]
  type: command
  name: Probe In
  gcode:
      PROBE_IN

  [menu __main __KlackEnder __AutoBedMesh]
  type: command
  name: Auto Bed Mesh
  gcode:
      G28
      AUTO_BED_MESH
  ```

### Marlin
The installation for Marlin requires some more changes, but I will guide you through this :)  There is also a zipped Marlin file. This is exactly the same configuration I used for testing. It contains the Probe related thins only!! Do not flash this to your printer!!

#### 1. Configuration.h

- Search for ```// @section homing``` (line 783) and change
  ```
  #define USE_XMIN_PLUG
  #define USE_YMIN_PLUG
  #define USE_ZMIN_PLUG
  //#define USE_IMIN_PLUG
  ```

  to 

  ```
  #define USE_XMIN_PLUG
  #define USE_YMIN_PLUG
  #define USE_ZMIN_PLUG
  #define USE_Z_MIN_PROBE_PIN     --> Remove // and add USE_Z_MIN_PROBE_PIN
  ```

- Search for ```// @section probes``` (line 1034) and change
  ```
  /**
  * Enable this option for a probe connected to the Z-MIN pin.
  * The probe replaces the Z-MIN endstop and is used for Z homing.
  * (Automatically enables USE_PROBE_FOR_Z_HOMING.)
  */
  #define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN
  ```

  to 

  ```
  /**
  * Enable this option for a probe connected to the Z-MIN pin.
  * The probe replaces the Z-MIN endstop and is used for Z homing.
  * (Automatically enables USE_PROBE_FOR_Z_HOMING.)
  */
  //#define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN      --> Add // to comment this out
  ```
  
- Search for ```Z_MIN_PROBE_PIN``` (line 1054) and change
  ```
  /**
  * Z_MIN_PROBE_PIN
  *
  * Define this pin if the probe is not connected to Z_MIN_PIN.
  * If not defined the default pin for the selected MOTHERBOARD
  * will be used. Most of the time the default is what you want.
  *
  *  - The simplest option is to use a free endstop connector.
  *  - Use 5V for powered (usually inductive) sensors.
  *
  *  - RAMPS 1.3/1.4 boards may use the 5V, GND, and Aux4->D32 pin:
  *    - For simple switches connect...
  *      - normally-closed switches to GND and D32.
  *      - normally-open switches to 5V and D32.
  */
  //#define Z_MIN_PROBE_PIN 32 // Pin 32 is the RAMPS default
  ```

  to 

  ```
  /**
  * Z_MIN_PROBE_PIN
  *
  * Define this pin if the probe is not connected to Z_MIN_PIN.
  * If not defined the default pin for the selected MOTHERBOARD
  * will be used. Most of the time the default is what you want.
  *
  *  - The simplest option is to use a free endstop connector.
  *  - Use 5V for powered (usually inductive) sensors.
  *
  *  - RAMPS 1.3/1.4 boards may use the 5V, GND, and Aux4->D32 pin:
  *    - For simple switches connect...
  *      - normally-closed switches to GND and D32.
  *      - normally-open switches to 5V and D32.
  */
  #define Z_MIN_PROBE_PIN 32 // Pin 32 is the RAMPS default   --> Remove // and add your Probe Pin. See the wiring guide for your pin.
  ```

- Search for ```Z_PROBE_ALLEN_KEY``` (line 1139) and change
  ```
  //
  // For Z_PROBE_ALLEN_KEY see the Delta example configurations.
  //
  ```

  to 

  ```
  /**
  * Allen key retractable z-probe as seen on many Kossel delta printers - https://reprap.org/wiki/Kossel#Automatic_bed_leveling_probe
  * Deploys by touching z-axis belt. Retracts by pushing the probe down. Uses Z_MIN_PIN.
  * 
  * NOTE by KevinAkaSam: See line 1194 at https://github.com/MarlinFirmware/Configurations/blob/release-2.0.9.3/config/examples/delta/generic/Configuration.h
  *        - The Y Position is set to -8 because the Y Endstop position is at -8. If you set your Y min position to 0, change it to 0 here as well.
  * 
  */
  #define Z_PROBE_ALLEN_KEY

  #if ENABLED(Z_PROBE_ALLEN_KEY)
  // 2 or 3 sets of coordinates for deploying and retracting the spring loaded touch probe on G29,
  // if servo actuated touch probe is not defined. Uncomment as appropriate for your printer/probe.

    #define Z_PROBE_ALLEN_KEY_DEPLOY_1 { 245, -8, 5 } //Move to side Dock
    #define Z_PROBE_ALLEN_KEY_DEPLOY_1_FEEDRATE XY_PROBE_FEEDRATE

    #define Z_PROBE_ALLEN_KEY_DEPLOY_2 { 245, -8, 0 } //Move down to probe / Attach probe
    #define Z_PROBE_ALLEN_KEY_DEPLOY_2_FEEDRATE (XY_PROBE_FEEDRATE)/10

    #define Z_PROBE_ALLEN_KEY_DEPLOY_3 { 245, -8, 20 } //Lift probe up
    #define Z_PROBE_ALLEN_KEY_DEPLOY_3_FEEDRATE XY_PROBE_FEEDRATE

    #define Z_PROBE_ALLEN_KEY_STOW_1 { 245, -8, 20 } // Move to dock
    #define Z_PROBE_ALLEN_KEY_STOW_1_FEEDRATE XY_PROBE_FEEDRATE

    #define Z_PROBE_ALLEN_KEY_STOW_2 { 245, -8, 0 } //Place probe into dock
    #define Z_PROBE_ALLEN_KEY_STOW_2_FEEDRATE (XY_PROBE_FEEDRATE)/10

    #define Z_PROBE_ALLEN_KEY_STOW_3 { 240, -8, 0 } //Small side move
    #define Z_PROBE_ALLEN_KEY_STOW_3_FEEDRATE XY_PROBE_FEEDRATE

    #define Z_PROBE_ALLEN_KEY_STOW_4 { 240, -8, 5 } //remove probe
    #define Z_PROBE_ALLEN_KEY_STOW_4_FEEDRATE XY_PROBE_FEEDRATE

    #define Z_PROBE_ALLEN_KEY_STOW_5 { 0, -8, 5 } //Move back to the left
    #define Z_PROBE_ALLEN_KEY_STOW_5_FEEDRATE XY_PROBE_FEEDRATE

  #endif // Z_PROBE_ALLEN_KEY
  ```

- Search for ```NOZZLE_TO_PROBE_OFFSET``` (line 1219) and change
  ```
  #define NOZZLE_TO_PROBE_OFFSET { 10, 10, 0 }

  // Most probes should stay away from the edges of the bed, but
  // with NOZZLE_AS_PROBE this can be negative for a wider probing area.
  #define PROBING_MARGIN 10
  ```

  to 

  ```
  #define NOZZLE_TO_PROBE_OFFSET { 8, 21, 1.2 }   --> set correct offset

  // Most probes should stay away from the edges of the bed, but
  // with NOZZLE_AS_PROBE this can be negative for a wider probing area.
  #define PROBING_MARGIN 15   --> more clearance to the sides of the bed.
  ```
  
- Search for ```// @section machine``` (line 1415) and change
  ```
  // The size of the printable area
  #define X_BED_SIZE 200
  #define Y_BED_SIZE 200

  // Travel limits (mm) after homing, corresponding to endstop positions.
  #define X_MIN_POS 0
  #define Y_MIN_POS 0
  #define Z_MIN_POS 0
  #define X_MAX_POS X_BED_SIZE
  #define Y_MAX_POS Y_BED_SIZE
  #define Z_MAX_POS 200
  ```

  to 

  ```
  // The size of the printable area
  #define X_BED_SIZE 235    --> adjust bed size
  #define Y_BED_SIZE 235    --> adjust bed size

  // Travel limits (mm) after homing, corresponding to endstop positions.
  #define X_MIN_POS 0
  #define Y_MIN_POS -8      --> adjust endstop position
  #define Z_MIN_POS 0
  #define X_MAX_POS 250     --> adjust x travel
  #define Y_MAX_POS Y_BED_SIZE
  #define Z_MAX_POS 250     --> adjust z travel
  ```
  
- Search for ```// @section calibrate``` (line 1548) and change
  ```
  //#define AUTO_BED_LEVELING_3POINT
  //#define AUTO_BED_LEVELING_LINEAR
  //#define AUTO_BED_LEVELING_BILINEAR
  //#define AUTO_BED_LEVELING_UBL
  //#define MESH_BED_LEVELING

  /**
  * Normally G28 leaves leveling disabled on completion. Enable one of
  * these options to restore the prior leveling state or to always enable
  * leveling immediately after G28.
  */
  //#define RESTORE_LEVELING_AFTER_G28
  //#define ENABLE_LEVELING_AFTER_G28
  ```

  to 

  ```
  //#define AUTO_BED_LEVELING_3POINT
  #define AUTO_BED_LEVELING_LINEAR    --> Remove //
  //#define AUTO_BED_LEVELING_BILINEAR
  //#define AUTO_BED_LEVELING_UBL
  //#define MESH_BED_LEVELING

  /**
  * Normally G28 leaves leveling disabled on completion. Enable one of
  * these options to restore the prior leveling state or to always enable
  * leveling immediately after G28.
  */
  #define RESTORE_LEVELING_AFTER_G28    --> Remove //
  //#define ENABLE_LEVELING_AFTER_G28
  ```
  
### 2. Configuration_adv.h

- Search for ```// Custom Menu: Main Menu``` (line 3853) and change
  ```
  // Custom Menu: Main Menu
  //#define CUSTOM_MENU_MAIN
  #if ENABLED(CUSTOM_MENU_MAIN)
    //#define CUSTOM_MENU_MAIN_TITLE "Custom Commands"
    #define CUSTOM_MENU_MAIN_SCRIPT_DONE "M117 User Script Done"
    #define CUSTOM_MENU_MAIN_SCRIPT_AUDIBLE_FEEDBACK
    //#define CUSTOM_MENU_MAIN_SCRIPT_RETURN   // Return to status screen after a script
    #define CUSTOM_MENU_MAIN_ONLY_IDLE         // Only show custom menu when the machine is idle

    #define MAIN_MENU_ITEM_1_DESC "Home & UBL Info"
    #define MAIN_MENU_ITEM_1_GCODE "G28\nG29 W"
    //#define MAIN_MENU_ITEM_1_CONFIRM          // Show a confirmation dialog before this action

    #define MAIN_MENU_ITEM_2_DESC "Preheat for " PREHEAT_1_LABEL
    #define MAIN_MENU_ITEM_2_GCODE "M140 S" STRINGIFY(PREHEAT_1_TEMP_BED) "\nM104 S" STRINGIFY(PREHEAT_1_TEMP_HOTEND)
    //#define MAIN_MENU_ITEM_2_CONFIRM

    //#define MAIN_MENU_ITEM_3_DESC "Preheat for " PREHEAT_2_LABEL
    //#define MAIN_MENU_ITEM_3_GCODE "M140 S" STRINGIFY(PREHEAT_2_TEMP_BED) "\nM104 S" STRINGIFY(PREHEAT_2_TEMP_HOTEND)
    //#define MAIN_MENU_ITEM_3_CONFIRM
  ```

  to 

  ```
  // Custom Menu: Main Menu
  #define CUSTOM_MENU_MAIN    --> Remove //
  #if ENABLED(CUSTOM_MENU_MAIN)
    #define CUSTOM_MENU_MAIN_TITLE "KlackEnder Commands"    --> Remove // and add menu title
    #define CUSTOM_MENU_MAIN_SCRIPT_DONE "M117 User Script Done"
    #define CUSTOM_MENU_MAIN_SCRIPT_AUDIBLE_FEEDBACK
    //#define CUSTOM_MENU_MAIN_SCRIPT_RETURN   // Return to status screen after a script
    #define CUSTOM_MENU_MAIN_ONLY_IDLE         // Only show custom menu when the machine is idle

    #define MAIN_MENU_ITEM_1_DESC "Probe Out"     --> Add macro name
    #define MAIN_MENU_ITEM_1_GCODE "G90\nG1 Z5\nG1 X245 F20000\nG1 Z0\nG4 P300\nG1 Z20\nG1 X0"    --> add script
    //#define MAIN_MENU_ITEM_1_CONFIRM          // Show a confirmation dialog before this action

    #define MAIN_MENU_ITEM_2_DESC "Probe In"    --> Add macro name
    #define MAIN_MENU_ITEM_2_GCODE "G90\nG1 Z20\nG1 X245 F5000\nG1 Z0 \nG4 P300\nG1 X240 F1000\nG1 Z5\nG4 P300\nG1 X0 F5000\nG1 Z0"   --> add script
    //#define MAIN_MENU_ITEM_2_CONFIRM

    #define MAIN_MENU_ITEM_3_DESC "Auto Bed Mesh"   --> Remove // and add macro name
    #define MAIN_MENU_ITEM_3_GCODE "G28\nG29\nG1 X0 Y0 F5000\nG1 Z0"    --> Remove // and add script
    //#define MAIN_MENU_ITEM_3_CONFIRM
  ```
