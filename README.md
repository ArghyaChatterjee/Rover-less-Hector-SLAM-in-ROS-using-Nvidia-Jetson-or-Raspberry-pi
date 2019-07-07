# Hector-SLAM-in-ROS-without-odometry
It's a Simultanous Localization And Mapping Technique in ROS which doesnot need any odometry data for realtime simulation in raspberry pi 3b or 3b+
# RPLidar Hector SLAM
Using Hector SLAM without odometry data on a ROS system with the RPLidar A1.

Install ROS full desktop version (tested on Kinetic) from: http://wiki.ros.org/kinetic/Installation/Ubuntu

Create a catkin workspace: http://wiki.ros.org/ROS/Tutorials/CreatingPackage

Clone this repository into your catkin workspace

In your catkin workspace run ```source /devel/setup.bash```

Run ```chmod 666 /dev/ttyUSB0``` or the serial path to your lidar

Run ```roslaunch rplidar_ros rplidar.launch```

Run ```roslaunch hector_slam_launch tutorial.launch```

RVIZ should open up with SLAM data
# Sources
RPLidar
Hector_SLAM
Fixing launch files (only needed if you are using the original hector slam repository)

In catkin_ws/src/rplidar_hector_slam/hector_slam/hector_mapping/launch/mapping_default.launch 
replace the second last line with 

```<node pkg="tf" type="static_transform_publisher" name="base_to_laser_broadcaster" args="0 0 0 0 0 0 base_link laser 100" />```

the third line with

```<arg name="base_frame" default="base_link"/>```

the fourth line with

```<arg name="odom_frame" default="base_link"/>```

In catkin_ws/src/rplidar_hector_slam/hector_slam/hector_slam_launch/launch/tutorial.launch 
replace the third line with

```<param name="/use_sim_time" value="false"/>```
