## KlackEnder Probe *Revision 2*

KlackEnder Probe - **Simple, fast and cheap!**
  
Adaptation of the [Klicky](https://github.com/jlas1/Klicky-Probe)/[Quickdraw](https://github.com/Annex-Engineering/Quickdraw_Probe) Probe for the Ender 3 and comparable         Creality printers. The probe is compatible with all printers that use the X plate of the Ender 3. The cost of the probe is <5€, of which the switch is the most expensive part.
The probe is compatible with **Marlin and Klipper**. Both firmwares work with the G29 command, the docking is done automatically by the printer, it couldn't be easier! Both    firmwares add a KlackEnder menu to the display that can be used to dock and undock the Probe. The Bed-Mesh can be created via the custom menu, via the default firmware settings or with G29.

**With the Rev2 you can replace the stock limit switch with the probe. This means you don't need an additional endstop port like for the Rev1.**

### Quick Overview:
- Compatible with Marlin and Klipper. Firmware is provided.
- Automatic docking and undocking of the probe.
- Custom menu to control the probe.
- Cheap way to get fast and accurate probing.
- Easy to install, no soldering.
- Works with all print surfaces
- **Use it as Z Endstop with the Rev2**

        
Its working very well for me. If you have any questions feel free to join the [Discord-Server](https://discord.gg/xqpKrxt9FC) 
 
<a href="https://discord.gg/xqpKrxt9FC">
         <img alt="Join" src="https://github.com/kevinakasam/BeltDrivenEnder3/blob/main/Pictures/Discord-Logo%2BWordmark-Color.png"
         width=250" >
      </a>

<table>
  <tr>
    <td><img src="https://raw.githubusercontent.com/kevinakasam/KlackEnder-Probe/main/Rev_2/Images/4.JPG" width="460"> </td>
    <td><img src="https://raw.githubusercontent.com/kevinakasam/KlackEnder-Probe/main/Rev_2/Images/3.jpg" width="460"> </td>
  </tr>
</table>

### BOM - Parts you need:
- 1x OMRON D2F or similar switch
- 6x Magnet 3x6mm 
- 1x M3x12-22mm screw (SHCS or BHCS doesn't matter)
- 2x M5x8mm screw (SHCS or BHCS doesn't matter)
- 2x M5 t-nut
- small zip tie and some cable (you may also need a connector to connect the probe to the mainboard e.g JST XH)
- Users of the Belt Z Mod: 1x M5x45mm screw (SHCS or BHCS doesn't matter) (with the wheels the 40mm screw is just long enough, for the MGN it's too short)
                                                                                                              
## STL-Files / Tolerances
<table>
  <tr>
    <td><img src="https://raw.githubusercontent.com/kevinakasam/KlackEnder-Probe/main/Rev_2/Images/ToleranceTest.png" width="460"> </td>
    <td><img src="https://raw.githubusercontent.com/kevinakasam/KlackEnder-Probe/main/Rev_2/Images/ToleranceTest1.png" width="460"> </td>
  </tr>
</table>

Some people have contacted me with the problem that the layers split when they insert the magnets. This happens when the magnet is too big for the hole/the hole is too small for the magnet. So either the magnets are a bit bigger than 6mm or your printer prints the holes too small (never use a caliper to measure the magnets!. Only if they are made of plastic!). How the printer prints the holes depends not only on the material (ABS shrinks a bit, while PETG stays fairly constant) but also on the orientation of the holes. Vertical holes are usually a bit smaller than the horizontal ones, the ones that are printed in the walls. This is because these holes are formed by the layers and can never be completely round (the circle is made of 0.2mm (layer height) lines). At the same time, the diameter is strongly influenced by the print settings (speed, acceleration, linear advance/pressure advance, etc.).

However, you may need different tolerances than I do. That is why I have designed a small tolerance test (_thanks to SchlongkyDong for the idea!_). As already described, the tolerances for vertical and horizontal holes can/will differ. Stick a screwdriver through the smaller holes to get your magnets out again.

### Parametric Fusion 360 File
There is an f3d file in the [CAD](https://github.com/kevinakasam/KlackEnder-Probe/tree/main/Rev_2/CAD) folder. This file format is for Autodesk Fusion 360, a free CAD program for private users. You can use it to adjust the tolerances if the STL files I provided do not fit.
As described in the tolerance test, there are different tolerances for vertical and horizontal holes. Follow the steps decribes in the [CAD](https://github.com/kevinakasam/KlackEnder-Probe/tree/main/Rev_2/CAD) folder to create your own STL.


## Assembly Guide
                                                                                                               
I will add a Video Guide soon! The assembly is very similar to the Rev1. You will have to insert an additinal magnet into the side of the `Probe_Block.stl`. There also belongs a magnet in the foremost hole of `Probe_Dock.stl` (looking at it when it's mounted). The M3 scew belongs into the rear hole (the thread will stick out of the dock and hold the Proble_Block in place.
                                                                                                               
                                                                                                               
---

## Wiring Guide
Since there is no polarity on Swichtes, it doesn't matter which wire goes where. Just connect the switch to the two marked pins.
In the next chapter about firmware changes you will see where to add the pin.

Wiring for the Rev2 is very easy. Simply unmount/unplug your old z-endstop and connect the probe to the z-endstop port.

## Firmware Guide
The KlackEnder probe works with Marlin and Klipper. This guide only shows you what changes you need to make to the firmware, not how to modify/upload the firmware itself. There are several guides online for different boards and printers.
**You do not have to use the ```Probe In``` or ```Probe Out``` macros.** They're just a nice to have. The printer will do this automatically when you send a ```G29```.


### Klipper

The installation for Klipper is pretty easy. Simply copy the code from the ```KlackEnder.cfg```to your ```printer.cfg```
The ```[gcode_macro G29]``` does the same like the ```[gcode_macro AUTO_BED_MESH]```. I just added this so you can use the G29 commend as usual.

**Don't forgot to edit your probe Pin:**
  ```
  ##################################
## Add this to your printer.cfg ##
################################## 
#####################################################################
#	KlackEnder- Settings
#####################################################################

# !! Change your Z endstop pin from 'endstop_pin: Pin123' to 'endstop_pin: probe:z_virtual_endstop'
# !! Also add in [stepper_y] 'position_min: -8'. Idk why but most configs mave this wrong. For the Stock Ender 3 the homed Y position is -8.

[probe]
pin: ^PC14 #Probe-Stop Connection on Skr Mini Pro V1.2
z_offset: -2 #Measure per your specific setup
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

[homing_override]
set_position_z:0 # Make printer think Z axis is at zero, so we can force a move upwards away from build plate
gcode:
    G90
    G1 Z10 F3000 ; move up to prevent accidentally scratching build plate    
    G28 X
    G28 Y
    PROBE_OUT
    G1 X117 Y117 F6000
    G28 Z
    PROBE_IN

##For Dual Z setups only!! (with indipendent motors, no Y splitters or dual Z port on board!)##
[z_tilt]
z_positions:
    0,117
    235,117
#   A list of X, Y coordinates (one per line; subsequent lines
#   indented) describing the location of each bed "pivot point". The
#   "pivot point" is the point where the bed attaches to the given Z
#   stepper. It is described using nozzle coordinates (the X, Y position
#   of the nozzle if it could move directly above the point). The
#   first entry corresponds to stepper_z, the second to stepper_z1,
#   the third to stepper_z2, etc. This parameter must be provided.
points:
    8,96.5
    215,96.5
#   A list of X, Y coordinates (one per line; subsequent lines
#   indented) that should be probed during a Z_TILT_ADJUST command.
#   Specify coordinates of the nozzle and be sure the probe is above
#   the bed at the given nozzle coordinates. This parameter must be
#   provided.
speed: 300
#   The speed (in mm/s) of non-probing moves during the calibration.
#   The default is 50.
horizontal_move_z: 15
#   The height (in mm) that the head should be commanded to move to
#   just prior to starting a probe operation. The default is 5.
retries: 10
#   Number of times to retry if the probed points aren't within
#   tolerance.
retry_tolerance: 0.01
#   If retries are enabled then retry if largest and smallest probed
#   points differ more than retry_tolerance. Note the smallest unit of
#   change here would be a single step. However if you are probing
#   more points than steppers then you will likely have a fixed
#   minimum value for the range of probed points which you can learn
#   by observing command output.

#####################################################################
#	KlackEnder- Macros
#####################################################################

[gcode_macro PROBE_OUT]
gcode:
    G90
    G1 X245 F4000
    G4 P300
    G1 Z15
    G1 X0

[gcode_macro PROBE_IN]
gcode:
    G90
    G1 Z20
    G1 X245 F20000
    G1 Y-8
    G1 Z0
    G4 P300
    G1 X220 F6000
    G1 Z10
    G1 X0

[gcode_macro AUTO_BED_MESH]
gcode:
    PROBE_OUT
    BED_MESH_CALIBRATE
    #G1 Y0 F20000
    PROBE_IN

[gcode_macro G29]
gcode:
    PROBE_OUT
    BED_MESH_CALIBRATE
    #G1 Y0 F20000
    PROBE_IN

[gcode_macro Accuracy_Test]
gcode:
    PROBE_OUT
    G90
    G1 Y120 X120 F20000
    PROBE_ACCURACY
    PROBE_IN

[gcode_macro AUTO_Z_TILT_ADJUST]
gcode:
    PROBE_OUT
    Z_TILT_ADJUST
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
The installation for Marlin requires some more changes, but I will guide you through this :). These changes are only to get the KlackEnder working correctly. You still need to configure the rest of the options as appropriate for your printer. Support for the KlackEnder and similar probes was only recently added so a current version of Marlin needs to be used. Go to ```https://marlinfw.org/meta/download/``` and download the ```2.1.x.zip```. Follow the instructions for downloading, Installing, and configuring VSCode. Before compiling with PlatformIO you will need to setup your config files. Go to ```https://github.com/MarlinFirmware/Configurations/tree/bugfix-2.1.x/config/examples/Creality``` find your Printer/board setup and down load the appropriate Configuration.h & Configuration_adv.h. At this point you will want to go through and make the changes below, once completed you should be good to compile and use your printer. We are working on getting Configuration files posted for common printer combinations as well as .bins uploaded.

Marlin will now include a probe deploy and stow option under the motion menu when the Mag_mounted probe is defined.

#### 1. Configuration.h
- Search for ``` #define Z_MIN_PROBE_USES_Z_MIN_ENDSTOP_PIN``` (line 1244) comment out by adding ```//``` before ```#define```

- Search for ```//#define USE_PROBE_FOR_Z_HOMING``` and uncomment by remvoving ```//``` before ```#define```

- Search for ``` //#define MAG_MOUNTED_PROBE``` (line 1349) uncomment by removing the ```//```
  and change lines 1354-1363 to 
  ```
  #define MAG_MOUNTED_DEPLOY_1 { PROBE_DEPLOY_FEEDRATE, { 245, 114, 30 } }  // Move to side Dock
  #define MAG_MOUNTED_DEPLOY_2 { PROBE_DEPLOY_FEEDRATE, { 245, 114, 0 } }  // Move down to probe / Attach probe
  #define MAG_MOUNTED_DEPLOY_3 { PROBE_DEPLOY_FEEDRATE, { 245, 114, 20 } }  // lift probe up
  //#define MAG_MOUNTED_DEPLOY_4 { PROBE_DEPLOY_FEEDRATE, {   0,   0,  0 } }  // Extra move if needed
  //#define MAG_MOUNTED_DEPLOY_5 { PROBE_DEPLOY_FEEDRATE, {   0,   0,  0 } }  // Extra move if needed
  #define MAG_MOUNTED_STOW_1   { PROBE_STOW_FEEDRATE,   { 245, 114, 20 } }  // Move to dock
  #define MAG_MOUNTED_STOW_2   { PROBE_STOW_FEEDRATE,   { 245, 114,  0 } }  // Place probe on dock
  #define MAG_MOUNTED_STOW_3   { PROBE_STOW_FEEDRATE,   { 240, 114,  0 } }  // Side move to remove probe
  #define MAG_MOUNTED_STOW_4   { PROBE_STOW_FEEDRATE,   { 240, 114, 20 } }  // Side move to remove probe
  //#define MAG_MOUNTED_STOW_5   { PROBE_STOW_FEEDRATE,   {   0,   0,  0 } }  // Extra move if needed
  ```
  Probe deploy and stow feedrate can be changed by edditing line's 1351-1352


- Search for ```NOZZLE_TO_PROBE_OFFSET``` (line 1453) and change
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
  
- Search for ```// @section machine``` (line 1661) and change
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
  #define X_BED_SIZE 230    --> adjust bed size
  #define Y_BED_SIZE 235    --> adjust bed size

  // Travel limits (mm) after homing, corresponding to endstop positions.
  #define X_MIN_POS 0
  #define Y_MIN_POS -8      --> adjust endstop position
  #define Z_MIN_POS 0
  #define X_MAX_POS +15     --> adjust x travel
  #define Y_MAX_POS Y_BED_SIZE
  #define Z_MAX_POS 250     --> adjust z travel
  ```
  
- Search for ```// @section calibrate``` (line 1806) and change
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
  //#define AUTO_BED_LEVELING_LINEAR
  //#define AUTO_BED_LEVELING_BILINEAR
  #define AUTO_BED_LEVELING_UBL     --> Remove //
  //#define MESH_BED_LEVELING

  /**
  * Normally G28 leaves leveling disabled on completion. Enable one of
  * these options to restore the prior leveling state or to always enable
  * leveling immediately after G28.
  */
  #define RESTORE_LEVELING_AFTER_G28    --> Remove //
  //#define ENABLE_LEVELING_AFTER_G28
  ```
  
- Search for ```Unified Bed Leveling``` line(1937)
  Change line 1942 from ```#define MESH_INSET 1```
  to ```#define MESH_INSET 10```
  
  Change line 1943 from ```#define GRID_MAX_POINTS_X 10```  
  to ```#define GRID_MAX_POINTS_X 15```  
  Uncomment line 1954 by removing the ```//``` before ```#define UBL_MESH_WIZARD```  
  Uncomment line 1974 ```//#define LCD_BED_LEVELING```  
  Uncomment Line 1983 ```//#define LCD_BED_TRAMMING```  
  Uncomment Line 1990 ```//#define BED_TRAMMING_USE_PROBE```  
  Uncomment Line 2048 ```//#define Z_SAFE_HOMING```
  Uncomment Line 2138 ```//#define EEPROM_INIT_NOW   // Init EEPROM on first boot after a new build```  
