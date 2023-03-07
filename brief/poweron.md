---
sort: 2
---

# Prepare befor power on

## zero position

**Make sure that the z1_ctrl program is turned off** before power on the robotic arm, 
otherwise there may be danger. 
And let the robotic arm stay in zero position. 
The zero position of the robotic arm is as shown in the figure below. 
The lines on both sides of the joint gaps of J1 and J6 correspond exactly, 
and the other joints can be placed in order.

<center>
<img src="../img/arm_powerOn.png" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Zero Position of Z1 Robotic Arm</div>
</center>
<br>

When the device is powered on successfully, 
the green light is steady on, and the blue light will flash once the self-check passes.

It should be noted that each joint of the robotic arm 
should be turned to the zero position before use every time, 
so that the theoretical zero position in the control algorithm 
coincides with the actual mechanical zero position. In addition, 
the black and white power cord of the motor at the end of the robotic arm has DC24V power supply. 
If it is not needed, be sure to wrap the black and white power cord 
with insulating tape to prevent danger such as short circuit.

```note
If the terminal prints 'Arm Version 3-8' after executing the 'z1_Ctrl -v', 
it's allowed to power on the robot in any position.

And the fisrt thing when power on is to press '~' key or execute 'backtostart'.
```

## Network configuration

The default IP address of the robotics arm is **192.168.123.110**. 
The users need to change the IP of the PC before control the robot.

### Change network segment

With the example of changing to **192.168.123.162**, run `ifConfig` in the terminal and you will find your port name. For example, enpxxx.

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

### Change the default IP address

Insert the telecommunication cable in the **auxiliary network port** of the robot arm, 
then execute `z1_controller/unitreeArmTools.py` in a terminal and enter command as prompted.

After that, power-on again.

## Singular Position

When the robotic arm is in a singular position, 
the degrees of freedom will degenerate 
and it will make the angular velocity of some joints to be infinite, 
and the robotic will be at the risk of losing control. 

It is recommended to run the robotic arm to the **forward point** after power-on to avoid this area.

<center>
<img src="../img/sigularity.png" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Singular Position of the Robotic Arm</div>
</center>
<br>
