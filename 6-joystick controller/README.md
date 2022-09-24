---
sort: 6
---

# Instructions for Using the Joystick to Control Z1

## Control Mode

There are three control modes using the joystick to control Z1.

1.Joint space control. The joystick can control every motor in this mode.

2.Cartesian space control. In this mode, Z1 robot arm acts as a whole, the joystick controls Z1 to move along the XYZ axis and rotate around the XYZ axis.

3.Fixed trajectory motion. Z1 robot arm has built-in fixed movements for demonstration.

## Introduction of Joystick Button

### Joint Space Control

When B1 robot stops, press **L1+L2 button at the same time** to switch to Z1 robot arm to be controlled, and B1 robot will no longer move. Then press R2 button to enter the joint space control mode. You can control individual joints by using the joystick as shown in the figure below. When Z1 robot arm finish the movement, press R2 to return it to its original position. 

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

When B1 robot stops, press **L1+L2 button at the same time** to switch to Z1 robot arm to be controlled, and B1 robot will no longer move. Then, or when Z1 robot arm is in the joint space control mode, press R1 button to enter the cartesian space control mode as shown in the figure below. When Z1 robot arm finish the movement, press R2 to return it to its original position. 

<center>
<img src="../img/joystick_cartesian control.png" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Cartesian Space Control</div>
</center>
<br>

<center>
<img src="../img/cartesian_example.jpg" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Robotic arm tool coordinate system</div>
</center>
<br>

### Fixed Trajectory Motion

When B1 robot stops, press **L1+L2 button at the same time** to switch to Z1 robot arm to be controlled, and B1 robot will no longer move. Then after pressing R1 button, press SELECT button to control Z1 robot arm to a fixed position. Then press SELECT button, Z1 will be back to the initial position, and the third time to press SELECT button, Z1 will always be in motion.

## Cautions

Since the B1 robot and the Z1 are controlled with the same joystick, there is a partial button sharing, therefore, when controlling the B1 robot movement, press **R1+R2 at the same time** to switch the Z1 robot arm into the passive state. To determine whether the Z1 is in the passive state, drag Z1 by hand; if it can be dragged, it is switch into the passive state. To control the movement of the robot arm, the B1 robot needs to be in the stop state.When Z1 robot arm finish the movement, press L1+L2 button at the same time to switch to B1 robot to be controlled.
