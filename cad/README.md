# Step Files
These files allow anyone to easily modify and improve the dARM physical design in almost any CAD software.

## dARM.zip
This is the entire robot arm.  It is zipped because the .step file was larger than the 100 MB github limit.

Contains:
+ Legs
+ 5 Large Actuators
+ Forearm
+ Gripper
+ All subcomponents

## dock.step
TPU dock that tightly fits the base and 3rd joint in the resting position.
+ Acts as zero position
+ Make `endstop switches` unnecessary
+ Acts as cusion for the 3rd joint during shutdown sequence

## fingers.step
Additional compliant finger designs. Each plate is labeled by version starting with v4.  v3 is included in dARM.step.

## powerBox.step
Housing for switching power supply, power monitor, display, and on/off switch.
+ Early version
    - lid just seats on box
    - relies on its own weight
