---
sort: 1
---

# Environment Construction

## Abstract

Both the robotic arm SDK and the robotic arm controller are based on Ubuntu 18.04, and the ROS system relied on in the simulation control is version Melodic. Therefore, for better operation, please keep it as consistent as possible. If you only use real machine control, no need to install ROS.

In addition, the robotic arm SDK and robotic arm controller also rely on many third-party tools, and users need to install these third-party tools before using them.

For the convenience, we also provide two library packages, **Eigen and RDBL**, in directory z1_sdk/ thirdparty/.After decompression, you can install directly according to the following steps. 

## Dependency Library Installation

+ build-essential

```shell
sudo apt install build-essential
```

+ Boost (Version 1.5.4 or higher)

```shell
dpkg -S /usr/include/boost/version.hpp      # check boost version
sudo apt install libboost-dev               # install boost
```

+ CMake (Version 2.8.3 or higher)
  
```shell
cmake --version                             # check cmake version
sudo apt install cmake                      # install cmake
```

+ GCC(GLIBCXX 3.4.22 or higher)

you can check the current version information of GLIBCXX with the following command.

```shell
strings /usr/lib/x86_64-linux-gnu/libstdc++.so.6 | grep GLIBCXX
```

upgrade

```shell
sudo add-apt-repository ppa:ubuntu-toolchain-r/test
sudo apt-get update
sudo apt-get install gcc-4.9
sudo apt-get upgrade libstdc++6
```

+ Eigen (version 3.3.9)

If old version Eigen has been installed, uninstall it first. If not, proceed to the next step.

Old Version Uninstall.

```shell
cd /usr/include
sudo rm -rf ./eigen3
```

Compilation and Installation

```shell
cd eigen-3.3.9
mkdir build
cd build
cmake ..
sudo make install

sudo ln -s /usr/local/include/eigen3  /usr/include/eigen3
sudo ln -s /usr/local/include/eigen3/Eigen  /usr/local/include/Eigen
```

<!-- + LCM (1.4.0版本)

```shell
cd lcm-1.4.0
mkdir build && cd build
cmake ..
make
sudo make install
``` -->

+ RBDL (Version 2.6.0)

```shell
cd rbdl-2.6.0
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE=release ..
sudo make install

sudo su    (input password)
echo /usr/local/lib >> /etc/ld.so.conf                      # set path
ldconfig
exit                                                        # Exit super administrator mode
```

## ROS(melodic) Installation

Refer to ROS official[melodic installation tutorial](http://wiki.ros.org/melodic/Installation/Ubuntu)

Add ROS Source

```shell
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```

Install Melodic

```shell
sudo apt update
sudo apt install ros-melodic-desktop-full
```

Install ROS Dependency

```shell
sudo apt-get install python3-pip 
sudo pip3 install rosdepc
sudo rosdepc init
rosdepc update
```

Add ROS Environment Variables

```shell
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```
## Network Configuration

### Change IP

The default IP of the robotic arm is 192.168.123.110. The users need to change the IP of the PC before using SDK.

With the example of changing to 192.168.123.162, run `ifConfig` in the terminal and you will find your port name. For example, enpxxx.

```shell
sudo ifconfig enpxxx down                                   # enpxxx is your PC port 
sudo ifconfig enpxxx 192.168.123.162/24 
sudo ifconfig enpxxx up 
```

The above method is to change the IP temporarily, you can also change the IP of the PC permanently, the operation please see below:

```shell
sudo vim /etc/network/interfaces
```

Add the following text to the interfaces file opened above.

```shell
auto enpxxx
iface enpxxx inet static
address 192.168.123.162
netmask 255.255.255.0
```

In this case, you can run the ping 192.168.123.110 command to check whether the connection with the robotic arm is normal.

### Change of Robotic Arm Control Program IP.

If the user changes the IP of the robotic arm control board, for example, changing the original 192.168.123.110 to 192.168.123.111, the IP address of the control program z1_crtl must be the same as the new one.

Open z1_controller/config.xml file and change the IP.

Another control parameter under this file is used to change the control mode of the robot arm, namely keyboard, SDK, and handle control of the two dogs. Users do not need to change, just use the SDK. (set = "2")

## Gripper Configuration

In config.xml, there are setting parameters for gripper. If you select 1, the end will have no gripper, and if it is 2, the end will be the Unitree gripper of the robotic arm.

This setting parameter is only configured in the program. The actual robot arm with or without gripper does not affect the execution of the program. z1_controller will give a warning when the parameters are inconsistent.

In the meanwhile, we allow users to define their own claw parameters according to user gripper, where endPosLocal is the relative coordinate of the gripper coordinates relative to the joint 5 terminal plane coordinate system (0.049, 0, 0.1605). The mass is the gripper mass, the unit is kg, com (center of mass) is the position of the gripper mass; I is the inertia matrix, which is uniformly distributed by default, so only values on the trace of the matrix are set.
