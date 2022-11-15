---
sort: 8
---

# Log Update

+ 2022.11.11

    1. Reduce the y-axis motion velocity in the singular region under Cartesian space.
    2. Move the config.xml to the config file and remove the config settings from it.

+ 2022.10.21

    1. Remove the gripper item from the file Config.xml, and instead detect the presence or absence of gripper according to the number of motors; add collision terms, including whether to turn on collision detection, limit torque and end load. The end load is attached to the end joint, which affects the calculation of the feedforward torque, and it is always in effect.
    2. Add error feedback to the communication structure between controller and SDK (need to be supported by the lower computer)
    3. Remove the controller's dependence on RBDL
    4. Remove keyboard control from SDK; Add lowlevelstate and lowlevelcmd classes to encapsulate UDP communication structures;

+ 2022.9.21

    1. Add end-effector control in State_Teach
    2. Add command track application in the State_JOINTCTRL and State_Cartesian

+ 2022.9.5
  
    1. Change the protocol transmission structure to allow users to customize multi-segment continuous traces.
    2. Solving the instability problem of rotation adjustment in cartesian space.

+ 2022.8.15

    1. Add end-effector configuration information in the config.xml.

+ 2022.8.12

    1. Temporarily add a non-gripper version SDK to solve the abnormal movement of the robotic arm caused by the error of non-gripper dynamics model in teaching mode.
