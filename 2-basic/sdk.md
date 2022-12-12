---
sort: 1
---

# Introduction to Robotic Arm SDK

Three files are provided for users to use z1 robot， which are `z1_controller`, `z1_sdk` and `unitree_ros`.

+ z1_controller: which stroes the code to control the z1 robot directly.
+ z1_sdk: which contains the interfaces used for z1 robot control.
+ unitree_ros: which contains the unitree products, includes Go1, A1, Aliengo , Laikago and z1 simulation files.

## 1. z1_controller

Apart form the files mentioned below, users do not need to view other files under this folder.

### 1.1 build/z1_ctrl

For the first time, users need to create "build" file and compile the program, and the resulting executable program is named `z1_ctrl`.

+ execute `./z1_ctrl -v` to check the version information
+ execute `./z1_ctrl k` to control the robot by keyboard
+ execute `./z1_ctrl` to control the robot by SDK

### 1.2 CMakeLists.txt

Choose to control the real robot or simulate by selecting UDP or ROS.

```cmake
Line8: set(COMMUNICATION UDP)
Line9: #set(COMMUNICATION ROS)
```

### 1.3 unitreeArmTools.py

This file is used to change the lower machine IP address (default: 192.168.123.110)

Use a cabek to connect the robot (**which needs to connect to the right backup network port**) and PC, then execute `python3 unitreeArmTools.py` and enter command as prompted.

### 1.4 config/config.xml

This file is read only once when `z1_ctrl` starts.

1. IP & Port

   **IP**：This refers to the robot lower machine IP address changed by `unitreeArmTools`, and when it has been changed, this parameter should be changed at the same time so that the `z1_ctrl` and the robot can communicate normally.

   **Port**：The port of the robot is **8880**, and this parameter is to change the native port bound when the PC performs the `z1_Ctrl`, the defalult is **8881**, which is used to control multiple robots on the same PC.

2. collision

    settings for collision check

    **open**: Whether open collision check by selecting Y or N

    **limitT**: The difference between torque and feedback torque , which calculates for collision check

    **load**: The end load is attached to the end joint, which affects the calculation of the feedforward torque, and it is always in effect.

### 1.5 config/saveArmStates.csv

This file is to save `label` for `labelRun()` and `labelSave()`, which represents the joint angles at that position.

## 2. z1_sdk

### 2.1 include

The forlder holds the header files of `unitree_arm_sdk`, and users can view the comments in it to understand what function does.

#### 2.1.1 unitree_arm_sdk/control

There are two files in it: `ctrlComponents.h` and `unitreeArm.h`.

`ctrlComponents.h` mainly puts all the control parameters in a class for easy calling. 

`unitreeArm.h` encapsulates all interfaces for controlling the robot.

#### 2.1.2 unitree_arm_sdk/model

This folder contains the armModel class, which contais functions suchas forward and inverse kinematics, inverse dynamics, and spatial Jacobial calculations of the robot.

The user can use these functions by calling `_ctrlComp->armModel` in the class `unitreeArm`.

## 2.2 examples

This folder contains three examples for the use of the `unitree_arm_sdk`.

### 2.2.1 highcmd_basic

If the user just wants to a simple understanding of how to control the robot, they can check out `highcmd_basic` file.

The example contains three methods for controling the robot.

① armCtrlByFSM()

The function controls the robot by calling the methods in the class `unitreeArm` directly, such as `MoveJ()`, `MoveL()`, `MoveC()`, `backToStart()`.

The function work as if the user use keyboard to control the robot with the './z1_ctrl k' command.

② armCtrlInJointCtrl()

The function is equivalen to further encapsulation on the basis of `highcmd_decelopment`. The user is only to control the direction of joint rotation instead of entering joint command $$q \And \dot{q}$$.

The following command calculation will be performed directlu in the function:

$$\dot{q} = directions*\omega$$  
$$q_{k} = q_{k-1} + \dot{q}*\delta t$$

And the function is equivalent to pressing `2` key when control by keyboard.

③ armCtrlInCartesian()

In cartesian space, the user was originally required to control the sptial velocity $$V = [\omega \quad v]'$$, that is, `unitreeArm.twist`  to control the robot, and the function was encapsulated on this basis. Then the user can directly control the direction in which the end of the robot was desired.

The following command calculation will be performed directly in the function:

where T is a homogeneous transformation matrix composed of R and p, and [ω] is the antisymmetric matrix of ω.

$$T_{\Delta} = directions * speed$$  
$$T_k = T_{\Delta} + T_{k-1}$$  
$$[\omega] = \log{(R_{k-1}^T R_k)}$$  
$$v=p_\Delta$$  

And the function is equivalent to pressing `3` key when control by keyboard.

### 2.2.2 highcmd_development

If user wants to control the robot through the planning trajectory, they can view this example.

This example writes a joint trajectory class `JointTraj`, where the `setJointTraj` and `setGripper` functions set the rajectory parameters (defined by the quintic polynomial) according to the given starting and the ending postion and speed, and `getJointCmd` will find the currently planned joint commands $$q$$ ad joint angulat velocity $$\dot{q}$$ according the execution time under different time parameter $$s \in [0, 1]$$

### 2.2.3 lowcmd_development

If the user wants to control the $$ q, \dot{q}, \tau_f, k_p, k_d $$ parameters of the motor directly, they can view this example.

This file shows how to send PD parameters directly to the motor. Users can control the motor by writing their own program to achieve independment development. The final output torque of the motor is as follows:

$$ \tau = k_p * 25.6 * (q_d - q) + k_d * 0.0128 * (\dot{q_d} - \dot{q}) + \tau_f$$

25.6 and 0.0128 are the scaling multiples in the communication protocol with the motor.

The `sendRecvThread` under `CtrlComponents` is a function that calls `unitreeArm` for instruction operations, such as running to forward as an instruction

And when running lowcmd, it is recommended to use its own defined thread, execute the `run` function, the run function starts to determine the command that needs to be sent to the motor through calculation, and finally calls sendRecv to send UDP packets.
