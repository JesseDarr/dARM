# dARM (dynamic Arm for Robitc Mischief)
dARM is a 3d printed 6 DOF robotic arm. Initially I wanted to create a 3d printed arm as a test of my new `Bambu X1C`. I found most existing projects used stepper motors.  I wanted a better power density.

So the dARM journey began. The goal was to design a cheap, powerful, robust, modular, and easily maintained arm from scratch using `ODrive S1` BLDC controllers.  It stands `.975 meters` tall, and can easily hold `5 lbs` in the horizontal position.

As I've itterated through various designs, modularity and maintenance became top priorities.  If any individual component fails, its modular section can be removed from the larger arm for easy replacement.

## Table of Contents
1. [Inspiration](#inspiration)
    - [James Burton](#james-burton)
    - [Skyentific](#Skyentific)
    - [OpenQDD](#openqdd)
    - [SSG48 Gripper](#ssg48-gripper)
2. [Design](#design)
    - [Control](#control)
    - [Power](#power)
    - [Mechanical](#mechanical)
        - [Primary Actuators](#primary-actuators)
        - [Forearm and Differential](#forearm-and-differential)
        - [Gripper](#gripper)
3. [Assembly](#assembly)

## Inspirations
Without the below projects and youtube channels the dARM project wouldn't exist.  I can't thank them enough for the inspiration and advice they've provided.

#### [James Burton](https://www.youtube.com/@jamesbruton)
What can I say about James.  I've been watching his channel for years.  Initially because he did interesting things with 3d printed parts, but shortly after that because the things he did were so consistently intersting.  James introduced me to ODrives as a control mechansim for BLDC motors.

#### [Skyentific](https://www.youtube.com/@Skyentific)
Another great youtuber.  He focuses on robotic arms, and mostly 3d printed robotic arms. He covers specifics of design, assembly, and controll for several different robot arms.  He also covers ODrives in great detail, including a video that uses a custom modified firmware to increase communication speed for specific queries over CAN.

#### [OpenQDD](https://www.aaedmusa.com/projects/openqdd)
The basis for the primary actuators are the OpenQDD by Aaed Musa.  Aaed also has an excellent [youtube channel](https://www.youtube.com/@aaedmusa). We use the same basic layout of an `8308 motor`, an `ODrive S1`, and a `planetary gearbox`. Our actuators have been redesigned from scatch to increased strength and rigidity, tigheten tolerances, print easier, and to have more robust mounting capabilities.

#### [SSG48 Gripper](https://source-robotics.github.io/SSG48-gripper-docs/page1_about_the_gripper)
The basis for the gripper is the SSG48 project.  We use a different motor, controller, and mounting dimensions, but we keep the basic motor housing layout, MGN7C rail/carriers, and a rack and pinion to move the fingers.

## Design

### Control

### Power

### Mechanical

#### Primary Actuators
These are the modular building block of joints 0-3. Each actuator use an `Eagle Power 8308 BLDC` motor mated to a 9:1 planetary gearbox. These come in 2 flavors: `single bearing` and `double bearing`.  

Double bearing actuators handle load perpindicular to the rotation axis better. They are used in joints that rotates on the vertical axis. 

Single bearing actuators are used in joints that rotate on the horizontal axis. **Note:** Joint 1 uses 2 single bearing actuators for increased power. This also eliminates the need for a doubl bearing actuator.

Below is an explode animation of each flavor.  They should give you a good idea of the sub components involved and are also a good assembly reference.

https://github.com/user-attachments/assets/06c78a0a-1a54-4e00-952e-c247763e0280

https://github.com/user-attachments/assets/b43786ba-b51d-407c-8697-83d8e092f9be

#### Forearm and Differential

https://github.com/user-attachments/assets/69bd7a27-f76a-4634-a556-fa9e3ffe39f6

#### Gripper

https://github.com/user-attachments/assets/7afa1675-455d-4928-a6e3-7bdbb0bead69

## Assembly
