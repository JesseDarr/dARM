# dARM (dynamic Arm for Robitc Mischief)
dARM is a 3d printed 6 DOF robotic arm. Initially, I wanted to build a 3d printed arm as a test of my new `Bambu X1C`. I found most existing projects used stepper motors.  I wanted a better power density.

https://github.com/user-attachments/assets/527a8380-1c22-4416-9524-2030928b34a5

So the dARM journey began. The goal was to design a cheap, powerful, robust, modular, and easily maintained arm from scratch using `ODrive S1` BLDC controllers.  It stands `.975 meters` tall and can easily hold `5 lbs` in the horizontal position.

After iterating through various designs, modularity and maintenence became top priorities.  If any individual component fails, its modular section can be removed from the larger arm for easy replacement.

## Table of Contents
1. [Versions](#versions)
2. [Inspirations](#inspirations)
    - [James Burton](#james-burton)
    - [Skyentific](#Skyentific)
    - [OpenQDD](#openqdd)
    - [SSG48 Gripper](#ssg48-gripper)
3. [Design](#design)
    - [Control](#control)
        - [Pi](#pi)
        - [CAN Wiring](#can-wiring)
    - [Power](#power)
    - [Mechanical](#mechanical)
        - [Primary Actuators](#primary-actuators)
        - [Forearm and Differential](#forearm-and-differential)
        - [Gripper](#gripper)
4. [Assembly](#assembly)

## Versions
Version numbers are determined purely by emotion. Don't ask what SDE stands for.

| Version   | Date          | Notes                             |
|---        | ---           | ---                               |
| 0.35 SDE  | 12/28/2024    | 6 axis, 7 motor design            |
| 0.45 SDE  | 1/17/2025     | Gripper v2 added                  |
| 0.55 SDE  | 1/28/2025     | Power Box added                   |
| 0.56 SDE  | 3/15/2025     | New gripper motor magnet holder   | 

## Inspirations
Without the below projects and youtube channels the dARM project wouldn't exist.  I can't thank them enough for the inspiration and advice they've provided.

#### [James Burton](https://www.youtube.com/@jamesbruton)
What can I say about James.  I've been watching his channel for years.  Initially, because he did interesting things with 3d printed parts, but shortly after that because the things he did were so consistently interesting.  James introduced me to ODrives as a control mechansim for BLDC motors.

#### [Skyentific](https://www.youtube.com/@Skyentific)
Another great youtuber.  He focuses on robotic arms, mostly 3d printed robotic arms. He covers specifics of design, assembly, and control for several different robot arms.  He also covers ODrives in great detail, including a video that uses a custom modified firmware to increase communication speed for specific queries over CAN.

#### [OpenQDD](https://www.aaedmusa.com/projects/openqdd)
The basis for the primary actuators are the OpenQDD by Aaed Musa.  Aaed also has an excellent [youtube channel](https://www.youtube.com/@aaedmusa). We use the same basic layout of an `8308 motor`, an `ODrive S1`, and a `planetary gearbox`. Our actuators have been redesigned from scatch to increase strength and rigidity, tighten tolerances, print easier, and to have more robust mounting capabilities.

#### [SSG48 Gripper](https://source-robotics.github.io/SSG48-gripper-docs/page1_about_the_gripper)
The basis for the gripper is the SSG48 project.  We use a different motor, controller, and mounting dimensions, but we keep the basic motor housing layout, MGN7C rail/carriers, and a rack and pinion to move the fingers.

## Control
The dARM is controlled with a `Raspberry Pi 4b` communicating to eight `ODrive S1s` via `CAN bus`.  This is achieved with the help of an `RS485 CAN Hat` on the Pi.  The ODrives are using the built in encoder with `encoder magnets` attached to each motor.

In a CAN network, the controller does not require a node ID, but each device on the network must have one. From this point forward, assume that the term "node" refers specifically to an ODrive and that node IDs are zero-indexed.

### Pi
The Pi is currently running Ubuntu 22.04 Server, but everything should still work with newer versions.  Instructions for install Ubuntu on a Pi can be found [here](https://ubuntu.com/tutorials/how-to-install-ubuntu-on-your-raspberry-pi#1-overview).  Set the hostname to `pidarm` and the username to `darm`.  Configure DHCP to connect to your wifi network.

#### Setup Commands
We need a static IP address so we can easily SSH into our PI.  This can be done in several ways, including this:

1. disable cloud-init networking
    - ```
     sudo echo "network: {config: disabled}" | sudo tee /etc/cloud/cloud.cfg.d/99-disable-network-config.cfg
     ```



### CAN Wiring
CAN wiring starts from the CAN Hat on the Pi.  A single `twisted pair` cable connects it to ODrive 0, which is then connected to ODrive 1, and so on with each ODrive daisy chained from the last like this:
```
         ┌─────────┐        ┌──────────┐     ┌──────────┐     ┌────────────┐
         │ CAN Hat ├───────►│ ODrive 0 ├────►│ ODrive 1 ├────►│ ODrive 2-7 │
┌────────└─────────┘┐       └──────────┘     └──────────┘     └────────────┘                        
│  Raspberry Pi 4b  │                                                                                        
└───────────────────┘                                                        
```

It's not well documented, but the ODrive S1 includes two `4-pin JST-GH` ports.  Each ODrive has 1 cable connected to the previous node and 1 cable connected to the next node.  It does not matter which port is used for which cable.  This allows us some freedom when we are building out our custom length cables.

<img src="https://github.com/JesseDarr/dARM/blob/main/pictures/odrive_s1_dip_switch.jpg" width="500">

Be sure to enabled the `120ohm resistor on ODrive 7` by flipping the `DIP Switch` to `120R`.  All other ODrives should have this DIP Switch set to `No R`. 

<img src="https://github.com/JesseDarr/dARM/blob/main/pictures/odrive_s1_jst_gh.jpg" width="500">

The BOM lists sacrifical 4pin JST-GH wires.  You will need to cut them in half and solder them into twisted pair.  You need to wire the twisted pair in a `roll over` fashion such that `PIN 2 is wired to PIN 2`, and `PIN 3 is wired to PIN 3`.  It is recommend to  solder 1 end connector onto the `tiwsted pair`, attach it to an ODrive, and then measure the required length of that cable.

The cable that connects the PI to ODrive 0 is a special case, it must also include a `PIN 4` for ground.  It should be wired into the `CAN Hat` like this:

<img src="https://github.com/JesseDarr/dARM/blob/main/pictures/rs485_can_hat.jpg" width="800">

## Power

- small    = 18 
- standard = 14

## Mechanical

### Primary Actuators
These are the modular building blocks of joints 0-3. Each actuator use an `Eagle Power 8308 BLDC` motor mated to a 9:1 planetary gearbox. These come in 2 flavors: `single bearing` and `double bearing`.  

Double bearing actuators handle load perpendicular to the rotation axis better. They are used in joints that rotates on the vertical axis. 

Single bearing actuators are used in joints that rotate on the horizontal axis. **Note:** Joint 1 uses 2 single bearing actuators for increased power. This also eliminates the need for a double bearing actuator.

Below is an explode animation of each flavor.  They should give you a good idea of the sub components involved and are also a good assembly reference.

https://github.com/user-attachments/assets/06c78a0a-1a54-4e00-952e-c247763e0280

https://github.com/user-attachments/assets/b43786ba-b51d-407c-8697-83d8e092f9be

### Forearm and Differential

https://github.com/user-attachments/assets/69bd7a27-f76a-4634-a556-fa9e3ffe39f6

### Gripper

https://github.com/user-attachments/assets/7afa1675-455d-4928-a6e3-7bdbb0bead69

## Assembly
