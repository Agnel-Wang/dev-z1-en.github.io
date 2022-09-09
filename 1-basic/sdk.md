---
sort: 1
---

# Introduction to Robotic Arm SDK

## File Structure 

All files about robotic arm SDK will be stored in a compressed package named z1_sdk_20xx.x.x.zip, Z1_sdk is the name of the SDK, and 20xx.x.x is the release date of SDK. There are three subfolders in the compressed package: z1_controller, z1_sdk and z1_ws, and z1_ws belongs to a workspace of the ROS system. Z1_controller stores the source codes which directly controls the robotic arm, the codes are packaged as a library and invisible to the user. Z1_sdk is a folder about the robotic arm named SDK unitree_arm_sdk, which contains the interfaces used for robotic arm control.

In folder z1_controller, the user only needs to focus on file CMakeLists.txt, and select ROS, UDP as required.

There are many subfolders in folder z1_sdk, and their functions are:	

+ Build:Folder where executable and intermediate files are stored when compiling for `unitree_arm_sdk`. (It is not included in the compressed package and needs to be created by the user.)
+ CMakeLists.txt:A file that guides `unitree_arm_SDK` compilation. If you write your own executable file, add a path to it.
+ examples:Source code files which stores the robotic arm controlling examples.
+ include:The header file that stores the `unitree_arm_SDK` source code. Users only need to include the unitree_arm_sdk/unitree_arm_sdk.h file in the source file.
+ unitreeArm:To store the source code of the unitreeArm class, which contains the methods that engineers encapsulate for users to easily call the robotic arm API. This class is closely related to the examples in the demo folder. Users can also use this type of code to write their own classes.

## examples

We have provided several examples to facilitate the use SDK. Please see the unitreeArm class comment for details.

### 1. example_keyboard_send

Users can send commands through the keyboard to control the robotic arm. The corresponding relationship between the specific keys and commands is described in the section of [Finite State Machine](FSM.md).

### 2. example_lowcmd_send

This file shows how to send **PD** parameters directly to the motor. The simulated parameters differ from the actual parameters.

### 3. bigDemo

bigDemo has written an example of calling member functions in the class by inheriting from the unitreeArm class.

### 4. getJointGripperState

The execution file prints the robotic arm end pose in real time to facilitate the user to record the point position.
