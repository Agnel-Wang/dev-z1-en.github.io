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

<!-- + GCC(GLIBCXX 3.4.22 or higher)

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
``` -->

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

<!-- + RBDL (Version 2.6.0, No required after version 2022.10.21)

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
``` -->

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

### Change of Robotic Arm Control Program IP.

If the user changes the IP of the robotic arm control board, for example, changing the original 192.168.123.110 to 192.168.123.111, the IP address of the control program z1_crtl must be the same as the new one.

Open z1_controller/config.xml file and change the IP.
