---
sort: 3
---

# Technical parameters

|Robot|Z1|
|:-:|:-:|
|DOF|6 rotation |
|Weight|4.1kg|
|Payload|≥3kg|
|Maximum reach|740mm|
|Repeatability|~0.1mm|
|Power supply|24V >20A|
|Communication|Ethenet|
|Programming|c++|

## Joints ranges

<center>
<img src="../img/range.png" style="zoom:70%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">The movement range of Z1 robotic arm</div>
</center>
<br>

## Coordinate

### Joint coordinate

<center>
<img src="../img/z1_arm_coordinate.png" style="zoom:70%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Joint Serial Number and Positive Direction of Joint Rotation Definition</div>
</center>
<br>

The serial numbers of its joints start from J1 and increase to J6 one by one. 
In the above figure, **key +** represents the positive direction of the joint rotation, 
and **key -** represents the negative direction. 

|Joint|ω|υ|
|:-:|:-:|:-:|
|J1|[0, 0, 1]|[0, 0, 0.065]|
|J2|[0, 1, 0]|[0, 0, 0.1115]|
|J3|[0, 1, 0]|[-0.35, 0. 0.1115]|
|J4|[0, 1, 0]|[-0.132, 0, 0.1685]|
|J5|[0, 0, 1]|[-0.06, 0, 0.1685]|
|J6|[1, 0, 0]|[-0.0128, 0, 0.1685]|

### Cartesian coordinate

<center>
<img src="../img/cartesian_example.jpg" style="zoom:70%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">Cartesian Space Control</div>
</center>
<br>

### Flange

<center>
<img src="../img/end flange.png" style="zoom:100%" alt=" 图片不见了。。。 "/>
<br>
<div style="color:orange; border-bottom: 0.1px solid #d9d9d9;
display: inline-block;
color: #999;
padding: 1px;">z1 Flange</div>
</center>
<br>

Where the absolute initial position of the gripper loading plane (the J6 end plane) is **[0,049, 0, 0.1605]**

The position of the center of the Unitree_gripper relative to the loading plane is **[0.0382, 0, 0]**.