# ROS-turtlebot3
BARAM ROS seminar KwangWoon University BARAM 2021 winter seminar Using URDF and turtlebot3 burger

## Requirements
-----------
ROS1 (melodic)
URDF
Rviz
Gazebo

## Installation
-----------
### URDF
```
sudo apt install ros-melodic-urdf
```
***
### Rviz
```
sudo apt install ros-melodic-rviz
```
***
### Gazebo
```
sudo apt install ros-melodic-gazebo-ros gazebo9(or gazebo11)
```
***

## Contents
-----------

```sh
├─scripts
│   | client.py   
│   | listener.py   
│   | server.py   
|   └─talker.py   
├─srv   
|   | PythonTest.srv   
| CMakeLists.txt   
| README.md   
└─package.xml   
```

## Descriptions
### Codes

1. client.py

```sh
    When we use rospy to create service, the "client.py" takes a role of "client". 
    
    So, it can request the service to server and receive the response.
    
    In this example, the "client" requests two integer numbers to server and waits for the sum of the two numbers. 
    
    It will terminate automatically After receive response.
```
