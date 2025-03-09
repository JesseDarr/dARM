# dARM (dynamic Arm for Robitc Mischief)

Purpose goes here.  
Pic or video

## Table of Contents
1. [Inspiration](#inspiration)
2. [Design](#design)
    - [Control](#control)
    - [Power](#power)
    - [Mechanical](#mechanical)
        - [Primary Actuators](#primary-actuators)
        - [Forearm and Differential](#forearm-and-differential)
        - [Gripper](#gripper)
3. [Assembly](#assembly)

## Inspirations

### [SSG48 Gripper](https://source-robotics.github.io/SSG48-gripper-docs/page1_about_the_gripper)
### [OpenQDD (Open Quasi Direct Drive)](https://www.aaedmusa.com/projects/openqdd)
### [James Burton](https://www.youtube.com/@jamesbruton)
### [Skyentific](https://www.youtube.com/@Skyentific)

## Design

### Control

### Power

### Mechanical

#### Primary Actuators
These are the modular building block of joints 0-3. Each actuator use an `Eagle Power 8308 BLDC` motor mated to a 9:1 planetary gearbox. These come in 2 flavors: `single bearing` and `double bearing`.  

Double bearing actuators handle load perpindicular to the rotation axis better. They are used in joints that rotates on the vertical axis. 

Single bearing actuators are used in joints that rotate on the horizontal axis.

Below is an explode animation of each flavor.  They should give you a good idea of the sub components involved and are also a good assembly reference.

https://github.com/user-attachments/assets/70e886fa-f724-4e31-8704-7430dc363660

https://github.com/user-attachments/assets/1fd90e32-2f6b-4316-a088-cb612336ff53


#### Forearm and Differential

#### Gripper

## Assembly