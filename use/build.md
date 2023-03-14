---
sort: 1
---

# Environment Construction

The motion control program can run on the Linux platform under the X86 architecture above Ubuntu 18.04.

Simulations can be run on ROS melodic or neotic versions.

## Dependency Library Installation

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
