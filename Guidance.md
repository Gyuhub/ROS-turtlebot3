Clone the repo of turtlebot3 which has the URDF file of turtlebot3 burger
```
1. cd ~/catkin_ws/src
2. git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3.git
3. cd ../ && catkin_make
```

Make the directory of workspace
```
1. cd ~/catkin_ws/src
2. catkin_create_pkg turtlebot_test roscpp rospy std_msgs
3. cd turtlebot_test
4. cd include && rm -r turtlebot_test
5. cd ../
```

Get turtlebot3 burger model
```
1. cd turtlebot3/turtlebot3_description/
2. cp -r urdf/ ../../turtlebot_test/
3. cp -r meshes/ ../../turtlebot_test/
4. cd ~/catkin_ws/src && sudo rm -r turtlebot3
```

Add burger model to environment
```
1. gedit ~/.bashrc
2. export TURTLEBOT3_MODEL=burger (제일 하단에)
3. save
4. source ~/.bashrc
```

Add world file to environment
```
1. cd ~/catkin_ws/src
2. git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
3. mkdir -p turtlebot_test/worlds/
4. cd turtlebot3_simulations/turtlebot3_gazebo/worlds/
5. cp turtlebot3_stage_3.world ~/catkin_ws/src/turtlebot_test/worlds/turtlebot3_stage_3.world
```

Add launch file to launch directory
```
1. cd ~/catkin_ws/src/turtlebot_test/
2. cd launch && touch turtlebot3_launch_test.launch
3. open the "turtlebot3_launch_test.launch" and add the below lines
```
**launch file**
```
<launch>
  <arg name="model" default="$(env TURTLEBOT3_MODEL)" doc="model type [burger, waffle, waffle_pi]"/>
  <arg name="x_pos" default="0.0"/>
  <arg name="y_pos" default="0.0"/>
  <arg name="z_pos" default="0.0"/>

  <include file="$(find gazebo_ros)/launch/empty_world.launch">
    <arg name="world_name" value="$(find turtlebot_test)/worlds/turtlebot3_stage_3.world"/>
    <arg name="paused" value="false"/>
    <arg name="use_sim_time" value="true"/>
    <arg name="gui" value="true"/>
    <arg name="headless" value="false"/>
    <arg name="debug" value="false"/>
  </include>

  <param name="robot_description" command="$(find xacro)/xacro --inorder $(find turtlebot_test)/urdf/turtlebot3_$(arg model).urdf.xacro" />

  <node pkg="gazebo_ros" type="spawn_model" name="spawn_urdf"  args="-urdf -model turtlebot3_$(arg model) -x $(arg x_pos) -y $(arg y_pos) -z $(arg z_pos) -param robot_description" />
</launch>
```