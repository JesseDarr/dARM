# Print Files
This project was designed to be printed on 256 x 256 build plate.  

The print files were created for a Bambu X1C and others high speed, high quality consumer printers.

All settings, including build plate specific customizations, are in a pro
file named `dARM`.  
All plates should be printed in `PLA+`, except the gripper fingers and dock which should be `TPU`.

## dARM.3mf
This is the entire robot arm.
+ 36 Plates
+ Plate names are descriptive and include the print count

Contains:
+ Legs
+ 5 Large Actuators
+ Forearm
+ Gripper
+ All subcomponents

## dock.3mf
TPU dock that tightly fits the base and 3rd joint in the resting position.
+ Acts as zero position
+ Make `endstop switches` unnecessary
+ Acts as cusion for the 3rd joint during shutdown sequence

## fingers.3mf
Additional compliant finger designs. Each plate is labeled by version starting with v4.  v3 is included in dARM.3mf.

## powerBox.3mf
Housing for switching power supply, power monitor, display, and on/off switch.
+ Early version
    - lid just seats on box
    - relies on its own weight