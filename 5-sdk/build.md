---
sort: 1
---

# Environment Construction

## Abstract

Both the robotic arm SDK and the robotic arm controller are based on Ubuntu 18.04, and the ROS system relied on in the simulation control is version Melodic. Therefore, for better operation, please keep it as consistent as possible. If you only use real machine control, no need to install ROS.

In addition, the robotic arm SDK and robotic arm controller also rely on many third-party tools, and users need to install these third-party tools before using them.

For the convenience, we also provide **Eigen** library packages, in directory z1_sdk/ thirdparty/. After decompression, you can install directly according to the following steps.

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

## ROS(melodic) Installation

Refer to ROS official[melodic installation tutorial](http://wiki.ros.org/melodic/Installation/Ubuntu)

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
