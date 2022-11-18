# Z1 Robot Arm

Welcome to use the Unitree Z1 robot arm and thank you for your purchase.

This document contains information about the installation and commissioning of the Z1 robot arm, and how to do secondary development based on the API.

<!-- **SDK下载链接**:

含Unitree手爪：<a href="downloads/z1_sdk.2022.8.11.zip" download>z1_sdk.2022.8.11</a>

无Unitree手爪：<a href="downloads/z1_sdk.2022.8.12.zip" download>z1_sdk.2022.8.12</a>

PS：用户需根据自身使用情况下载相应的SDK。 -->

<!--## Safety instructions

###	Introduction

Robotic arm users should fully understand the risks, must read this manual carefully before use, and strictly comply with the specifications and requirements in the manual. Unitree Technology is committed to providing excellent products, but due to the high risk of robotic arms, even if all operations are used in accordance with the instructions in the manual, there is no guarantee that it will not cause damage to persons and property, Unitree Technology is not responsible for this.

## Cautions

1. Be sure to follow the requirements in this manual to install the robot arm and connect the cables

2. Ensure that the robot arm does not collide with people or other objects within its range of activity to avoid accidents

3. Before use, need professional personnel to debug

4. When using the SDK, make sure the input parameters and operation process are correct

5. The robot arm will generate heat during operation, please do not touch the robot arm when it is running or just stopped.

6. Please pay attention to the operation speed of the robot arm, and be careful when it is too fast.

7. Please be sure to disconnect the power after the arm is used.

8. Avoid using the arm in wet or dusty environment.

9. Please make sure to store and install the arm in a place where children cannot touch it to avoid danger.-->

## Abstract

Z1 can realize various upper-level control modes such as joint space control, Cartesian space control, etc. It can also realize the low-level control of the underlying joint motors, based on which users can develop their own control algorithms. To achieve the above control relies on the use of the robotic arm SDK. There are currently two ways to control the robotic arm through the robotic arm SDK.

+ **Code Control**
You can write C++ programs to call the robotic arm development interface to control the robotic arm.
+ **Keyboard control**
The robotic arm can be controlled directly from the keyboard.

The robotic arm SDK also supports physical control and simulation control, where the simulator used for simulation control is Gazebo.

## File Structure


Z1 package contains three files。
Download：[![file](https://img.shields.io/badge/Z1-controller-green)](https://github.com/unitreerobotics/z1_controller) [![file](https://img.shields.io/badge/Z1-sdk-green)](https://github.com/unitreerobotics/z1_sdk) [![file](https://img.shields.io/badge/Z1-ros-green)](https://github.com/unitreerobotics/z1_ros)

+ z1_controller

This folder contains the control implementation part of the robot arm.

+ z1_sdk

This folder contains the interface to the control program.

+ z1_ros

This folder contains the files related to the ROS simulation model.

<center>
<img src="img/relation.png" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Relationship Map</div>
</center>
<br>

As shown in the figure, the robot arm's controller `z1_ctrl` issues commands to the robotic arm in gazebo through the ros system during the simulation control. In the physical control, commands are issued to the physical arm via udp, and the arm-related status, such as joint information and end position, is returned to `z1_ctrl` in the same way.The robotic arm sdk `unitree_arm_sdk` sends the user's control commands to `z1_ctrl` via udp, while `z1_ctrl` feeds the status information returned by the robot arm to `unitree_arm_sdk` via udp, and the user gets the relevant information by reading the relevant structures.
Therefore, because of the above-mentioned relationship between the three, the actual user start-up process should be

1. Start `robotic arm`: If it is physically controlled, check whether the mechanical part is powered on successfully and whether the device bule light is flashing. If it is emulation control, check if the `roslaunch z1_gazebo z1.launch` command is started.

2. Start `z1_ctrl`

3. Start `unitree_arm_sdk`
