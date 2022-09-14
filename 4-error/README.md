---
sort: 4
---

# Common Abnormalities  

## Vibration of Robotic Arm

To ensure the force control capability of the robotic arm, the deceleration ratio of harmonic reducer used in each joint is relatively low, which makes the joint stiffness in the same situation. And the robotic arm is light weighted, the connecting rod is also light, so the mechanical stiffness of the robotic arm is relatively low.Therefore, if the control method adopted is not optimized enough, the robotic arm may shake.

## Motor Over-temperature Protection

If the load of robotic end is large and its continuous operation time is too long, with different pose, the joints with a large load will make the joint motor overheat and enter the protection state.

## Joint not Reset when Power-on

If the following error occurs when the robotic arm is powered on, it is because the joint 1 is not at the zero position when the robotic arm is powered on. Therefore, be sure to place all joints of the robotic arm to the zero position before powering on.

```text
[ERROR] The No.1 term of joint angle: -0.024 does not between [0.000 3.142]
```

## Direct replacement of PC cannot control the robot arm when the arm is not powered

 Z1 robot arm will automatically bind the port after powering on and communicating with PC, so to replace the computer-controlled robot arm, you need to power off and power on the robot arm again.

## The red light of Z1 robot arm indicator flashes

There is an abnormality in the robotic arm joint communication.

## The third joint suddenly moves at the end of Z1 robot arm dragging demonstration

The angle of the third joint dragged during the demonstration exceeds the software limit.

## Entering the dragging demonstration mode, the third joint of Z1 robot arm suddenly pops up

This problem is caused by a kinetic model error. If the robot arm has no gripper, you need to set the "gripper set" to 1 in config.xml under z1_controller folder. The SDK defaults to a kinetic model with gripper.
