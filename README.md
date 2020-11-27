RPLIDAR ROS package
=====================================================================

ROS node and test application for RPLIDAR

Visit following Website for more details about RPLIDAR:

rplidar roswiki: http://wiki.ros.org/rplidar

rplidar HomePage:   http://www.slamtec.com/en/Lidar

rplidar SDK: https://github.com/Slamtec/rplidar_sdk

rplidar Tutorial:  https://github.com/robopeak/rplidar_ros/wiki

How to build rplidar ros package
=====================================================================
    1) Clone this project to your catkin's workspace src folder
    2) Install Foxy ROS2 and colcon compiler.
```
source /opt/ros/foxy/setup.bash
rosdep install -i --from-path src --rosdistro foxy -y
colcon build --symlink-install --packages-select rplidar_ros
```
How to run rplidar ros package
=====================================================================
There're two ways to run rplidar ros package

I. Run rplidar node and view in the rviz
------------------------------------------------------------
`ros2 launch rplidar_ros view_rplidar.launch` (for RPLIDAR A1/A2)
,
`ros2 launch rplidar_ros view_rplidar_a3.launch` (for RPLIDAR A3)
or
`ros2 launch rplidar_ros view_rplidar_s1.launch` (for RPLIDAR S1)

You should see rplidar's scan result in the rviz.

II. Run rplidar node and view using test application
------------------------------------------------------------
`ros2 launch rplidar_ros rplidar.launch` (for RPLIDAR A1/A2)
,
`ros2 launch rplidar_ros rplidar_a3.launch` (for RPLIDAR A3)
or
`ros2 launch rplidar_ros rplidar_s1.launch` (for RPLIDAR S1)

`ros2 run rplidar_ros rplidar_composition`

You should see rplidar's scan result in the console

Notice: the different is serial_baudrate between A1/A2 and A3/S1

RPLidar frame
=====================================================================
RPLidar frame must be broadcasted according to picture shown in rplidar-frame.png
