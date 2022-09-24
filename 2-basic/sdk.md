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

By inheriting from the unitreeArm class, bigDemo writes an example of calling a member function in the class.

Four functions are defined in the Z1 ARM class to demonstrate each of the four ways to control the robot arm using upper-level commands.

```cpp
    void armCtrlByFSM();
    void armCtrlByTraj();
    void armCtrlTrackInJointCtrl();
    void armCtrlTrackInCartesian();
```

① void armCtrlByFSM()

*armCtrlByFSM* implements specific application  by switching the state machine.

For example, through the *MoveJ(posture)* function, you can automatically switch to the *MoveJ* state machine and run to the specific posture.

Note: In this way, *MoveJ*、*MoveL* and *MoveC* do not have speed definition interface.

② void armCtrlByTraj()

This function involves two state machines, **State_Trajectory** and **State_SetTraj**.

By switching to State_SetTraj (which must be in the State_JOINTCTRL) via the *setTraj()* function automatically, and recording the currently TrajCmd,
(trajOrder must be guaranteed to be continuous), where the start point of the trajectory is the end point of the previous trajectory. All trajectories will be recorded while exiting the State_SETTRAJ, and then you can enter the State_Trajectory to execute the recorded trajectories in turn.

If a new trajectory is not set by State_SetTraj during this process, you can enter the State_Trajectory again to execute the recorded trajectory.

```text
Note: Since the state machine in the SDK is switched by simulating the keyboard, 
the two state machines also have actual corresponding keys in the keyboard, which are "-" and "l", respectively.
But in fact, it is impossible to do anything simply through the keyboard. 
However, if the user presses the minus "-" key in the keyboard, the robot arm will run a default demonstration action.

At the same time, if the bigdemo is running at State_Trajectory, given the command has been sent, 
the z1_ctrl will still complete the execution of the current trajectory even if the bigdemo program has been terminated.
```

③ void armCtrlTrackInJointCtrl()

This function runs under the State_JOINTCTRL, there is a flag named "track", under normal circumstances the value is false, you can press keys to control the movement of the robotic arm through keyboard control method, but can not be operated during programming.  When flag track is set to true, the robotic arm runs with the q and qd commands in jointCmd until flag track is set to false again.

④ void armCtrlTrackInCartesian()

This function runs under the State_Cartesian, which is same as armCtrlTrackInJointCtrl(), but tracking commands change from jointCmd.q and jointDmd.qd to trajCmd.posture[0].

### 4. getJointGripperState

The execution file prints the robotic arm end pose in real time to facilitate the user to record the point position.
