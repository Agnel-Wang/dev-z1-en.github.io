---
sort: 2
---

# SDK Operation

## ROS Simulation

**①** Set ros workspace

If the user is not familiar with the path setting, please create the folder named `unitree_ws/src` and move folder `unitree_ros` folder in it, which shoud be `~/unitree_ws/src/unitree_ros`.
Then download the folder [unitree_legged_msgs](https://github.com/unitreerobotics/unitree_ros_to_real), move it to `~/unitree_ws/src/`.

```shell
cd ~/unitree_ws                                                         #Open the folder
catkin_make                                                             #Initialize ROS workspace
echo “source ~/unitree_ros/devel/setup.bash”>>~/.bashrc #Add the ros path to the environment variables
source ~/.bashrc                                                        #Update environment variables
```

Run `roslaunch unitree_gazebo z1.launch`, If successfully configured, the simulation interface of Gazebo will be displayed.

```text
Tips：After entering `RosLaunch Z`, press tap to check whether the terminal will automatically complete. If rosLaunch Z1_ is successfully programmed, that means the path setting is successful.
```

**②** Open the CMakeLists in the z1_controller folder and change the compilation conditions as follows.

```cmake
# set(COMMUNICATION UDP)             #UDP
set(COMMUNICATION ROS)               #ROS
```

**③** Compile z1_controller, create a folder named build in this file (open the second terminal).

```shell
mkdir build
cd build
cmake ..
make
```

Execute the executable file `./z1_ctrl` in folder build. The default control mode is SDK, if you need to use keyboard control, use `./z1_ctrl k`

When executing this command, the terminal will continuously print statements, such as`[WARNING] UDPPort::recv, unblock version, wait time out`, this is normal because we have not started the robotic arm SDK to communicate with the robotic arm controller.

**Various information will be printed in this window, please observe the content of this window.**

**④** Open folder z1_SDK and create folder build in it (open the third terminal).

```shell
mkdir build
cd build
cmake ..
make
```

Execute the executable file in folder build.

There are two executable files generated, example_lowcmd_send and bigdemo.

This time we run bigdemo.

```shell
./highcmd_basic
```

+ Keyboard Operation:The specific keys will be introduced in state machine section.

First press `2` on the keyboard and then press key `0`, the robotic arm will enter the label operation state machine. Input forward at the prompt, then click enter, the robotic arm will run forward. Press `~` again, return to the origin. After returning to the origin, it will automatically enter the joint control mode. At this time, the rotation of the robotic arm can be controlled by **long press** according to the following keys.

<table border="1">
    <tr>
        <td>Joint ID</td>
        <td>0</td><td>1</td><td>2</td><td>3</td><td>4</td><td>5</td>
        <td>Gripper</td>
    </tr>
    <tr>
        <td>Keyboard</td>
        <td>Q/A</td><td>W/S</td><td>D/E</td><td>R/F</td><td>T/G</td><td>Y/H</td>
        <td>up/down</td>
    </tr>
    <tr>
        <td><p>Joint Action</p>(right hand)</td>
        <td><p>positive/</p>negative</td><td><p>positive/</p>negative</td>
        <td><p>positive/</p>negative</td><td><p>positive/</p>negative</td>
        <td><p>positive/</p>negative</td><td><p>positive/</p>negative</td>
        <td><p>positive/</p>negative</td>
    </tr>
</table>

Now, we have completed the simulation operation. The whole process is: **Run ROS-->Run z1_ctrl-->Run SDK instance**.

## Real Machine Control

**①** First power on the robotic arm, and check whether the communication is normal by ping 192.168.123.110 command.

**②** Open file CMakeLists in folder z1_controller and change the compilation conditions as follows.

```cmake
set(COMMUNICATION UDP)                         #UDP
# set(COMMUNICATION ROS)                       #ROS
```

**③** Run `./z1_ctrl`
**④** Run `./highcmd_basic`

The operation here is consistent with the simulation. Now, we have learned how to control the robotic arm. More operation methods will be introduced in the [basic concept](../2-basic/sdk.md) section.

## Multiple robots control

**<1>** open the directory z1_controller, set `Communication` in CMakeLists.txt to **UDP**,

copy the directory z1_controller, named as z1_controller_111

**<2>** open the directory z1_controller_111

**①** main.cpp

set UDP port (Line51) as shown in the following example:

```cpp
ctrlComp->cmdPanel = new ARMSDK(events, emptyAction, "127.0.0.1", 8074, 8073, 0.002);
```

**②** config.xml

set `IP` to "192.168.123.111", set `Port` to 8882

**③** unitreeArmTools.py

set the second robotic arm IP to 192.168.123.111.

**<3>** As described previously, proceed as follows:

1. execute z1_ctrl in **z1_controller** at the first terminal, which communicates with the robotic arm 110.
2. execute z1_ctrl in **z1_contrller_111** at the second terminal, which communicates with the robotic arm 111.
3. execute lowcmd_multirobots in **z1_sdk** at the third terminal.

And then we can see that the Joint1 of both robotic arm has turned at an angle.
