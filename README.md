# Z1

欢迎您使用Unitree机械臂，并感谢您的购买。

本文档记载了有关Z1机械臂的安装、调试、以及如何基于API进行二次开发的相关信息。

在使用本产品前，请仔细阅读本文档。

PS：如果您第一次使用本产品，可以先阅读第三小节[SDK使用](3-sdk/)

<!-- **SDK下载链接**:

含Unitree手爪：<a href="downloads/z1_sdk.2022.8.11.zip" download>z1_sdk.2022.8.11</a>

无Unitree手爪：<a href="downloads/z1_sdk.2022.8.12.zip" download>z1_sdk.2022.8.12</a>

PS：用户需根据自身使用情况下载相应的SDK。 -->

## 概要

宇树机械臂可以实现关节空间控制、笛卡尔空间控制等多种上层控制模式，还可以实现对底层关节电机的底层控制，用户可以基于此开发自己的控制算法。要实现上述控制则依赖于机械臂SDK的使用。目前通过机械臂SDK对机械臂的控制方式有两种：

+ **程序代码控制** \
可以通过编写C++程序来调用机械臂开发接口来控制机械臂。
+ **键盘控制** \
可以通过键盘直接地控制机械臂。

机械臂SDK还支持对机械臂的实物控制和仿真控制，其中仿真控制使用的仿真器是Gazebo。

## 文件结构

关于机械臂SDK的文件存储在z1_sdk.20xx.x.x.zip文件夹中，其中20xx.x.x为该SDK发布日期。

该压缩包中包含三个子文件：z1_controller、z1_sdk及z1_ws。

+ z1_controller

该文件夹包含了机械臂的控制实现部分。

+ z1_sdk

该文件夹包含控制程序的接口。

+ z1_ws

该文件夹属于ROS的一个工作空间，其中z1_ws/src/z1_ros文件夹下包含了ROS仿真模型的相关文件。

<center>
<img src="img/relation.png" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">关系图</div>
</center>
<br>

如图所示，在仿真控制时机械臂的控制器`z1_ctrl`通过ros系统对gazebo中的机械臂发布命令进行控制，在实物控制中则通过udp对实物机械臂发布命令进行控制，而机械臂相关的状态(如：关节信息、末端位姿等)则通过同样的方式返回至`z1_ctrl`。机械臂sdk`unitree_arm_sdk`通过udp将用户的控制命令(不管是上层控制命令还是底层控制命令)发送至`z1_ctrl`，同时`z1_ctrl`将机械臂返回的状态信息通过udp反馈至`unitree_arm_sdk`，用户通过读取相关结构体获取相关信息。\
&emsp;&emsp;故因为这三者存在上述所述关系，用户在实际使用时的启动流程应是：

1. 启动`机械臂`：如是实物控制，则检查机械部是否上电成功和设备灯是否闪烁。若是仿真控制，则检查是否启动`roslaunch z1_gazebo z1.launch`命令(下文介绍)。

2. 启动`z1_ctrl`

3. 启动`unitree_arm_sdk`
