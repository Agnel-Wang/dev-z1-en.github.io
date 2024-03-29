---
sort: 5
---

# Unitree Joystick Control

## Control Mode

There are three control modes using the joystick to control Z1.

1.Joint space control. The joystick can control every motor in this mode.

2.Cartesian space control. In this mode, Z1 robot arm acts as a whole, the joystick controls Z1 to move along the XYZ axis and rotate around the XYZ axis.

3.Fixed trajectory motion. Z1 robot arm has built-in fixed movements for demonstration.

## Introduction of Joystick Button

### Joint Space Control

+ B1

When B1 robot stops, press **L1+L2** button at the same time to switch to Z1 robot arm to be controlled, and B1 robot will no longer move. Then press **R2 button** to enter the joint space control mode. You can control individual joints by using the joystick as shown in the figure below. After the movement is finished, if you want the Z1 robot arm to keep the current attitude still, you can press **L2+R2** at the same time, and the robot arm will no longer receive the control information from the joystick. Then you can press **L1+L2** to control B1 robot while keeping the Z1 robot arm in the current posture. When B1 robot stops, press **L1+L2** button at the same time to switch to Z1 robot arm to be controlled, and B1 robot will no longer move. Then press **R2 button** to continue to control the Z1 robot arm. When Z1 robot arm finish the movement, press **SELECT** to return it to its original position. 


<center>
<img src="../img/joystick_joint control.png" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Joint Space Control</div>
</center>
<br>

### Cartesian Space Control

When B1 robot stops, press **L1+L2** button at the same time to switch to Z1 robot arm to be controlled, and B1 robot will no longer move. Then, or when Z1 robot arm is in the joint space control mode, press **R1** button to enter the cartesian space control mode as shown in the figure below. After the movement is finished, if you want the Z1 robot arm to keep the current attitude still, you can press **L2+R2** at the same time, and the robot arm will no longer receive the control information from the joystick. Then you can press **L1+L2** to control B1 robot while keeping the Z1 robot arm in the current posture. When B1 robot stops, press **L1+L2** button at the same time to switch to Z1 robot arm to be controlled, and B1 robot will no longer move. Then press **R2 or R1** button to continue to control the Z1 robot arm. When Z1 robot arm finish the movement, press **SELECT** to return it to its original position. 

<center>
<img src="../img/joystick_cartesian control.png" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Cartesian Space Control</div>
</center>
<br>

<!-- <center>
<img src="../img/cartesian_example.jpg" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Robotic arm tool coordinate system</div>
</center>
<br> -->

### Fixed Trajectory Motion

When B1 robot stops, press **L1+L2** button at the same time to switch to Z1 robot arm to be controlled, and B1 robot will no longer move. Press the **R2** button to enter the joint space control, then press the **R2+X** combination button at the same time the robot arm will enter the preset fixed trajectory movement. Press **SELECT** to return it to its original position. 

## Cautions

Since the B1 robot and the Z1 are controlled with the same joystick, there is a partial button sharing, therefore, when controlling the B1 robot movement, press **R1+R2** at the same time to switch the Z1 robot arm into the passive state or press **L2+R2** at the same time to keep the Z1 robot arm in the current posture. To determine whether the Z1 is in the passive state, drag Z1 by hand; if it can be dragged, it is switch into the passive state. To control the movement of the robot arm, the B1 robot needs to be in the stop state.

## log update

+ 2022.1.5

    1. Key mapping optimization.
    2. Add new function of adjusting speed for joint and cartesian space control.
    3. Add new function of controlling B1 robot while keeping Z1 robot arm in a fixed posture.
    4. Replace the **L1+L2** button with the **R1+R2** button to switch the Z1 robot arm into the passive state.

+ 2022.10.19

    1. Replace the **R2** button with the **SELECT** button to return the robot arm to the original position.
    2. The **SELECT** button no longer controls the robot arm to make fixed trajectory movements, and is replaced by the **R2+X** combination button.
    3. Replace the **R1+R2** button with the **L1+L2** button to switch the Z1 robot arm into the passive state.

+ 2022.9.14

    1. Preliminary Draft.
