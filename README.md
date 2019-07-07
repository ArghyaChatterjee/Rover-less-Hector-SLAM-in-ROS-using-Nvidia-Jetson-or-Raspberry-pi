# Hector-SLAM-in-ROS-without-odometry-data
  It's a Simultanous Localization And Mapping Technique in ROS which doesnot need any odometry data for realtime simulation   in nvidia jetson nano, raspberry pi 3b, 3b+ & 4.
# Ubuntu Mate 16.04 setup in raspberry pi
  Go to this website and follow the tutorial: https://downloads.ubiquityrobotics.com/pi.html
# Ubuntu 16.04 setup in Nvidia Jetson Nano
  Go to this website and follow the tutorial: https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit
# ROS Download
  Install ROS full desktop version (tested on Kinetic) from: http://wiki.ros.org/kinetic/Installation/Ubuntu & Create a catkin workspace: http://wiki.ros.org/ROS/Tutorials/CreatingPackage

# RPlidar SDK Download & Communicating with the port
  1. After plugging in the RPlidar to USB port of your device, in your terminal, run 
  ```usb-devices```
  2. If you see ```.....Product=CP2102 USB to UART Bridge Controller...If#= 0 Alt= 0 #EPs= 2 Cls=ff(vend.) Sub=00 Prot=00   Driver=cp210x```then the driver is preinstalled in your system.
  3. If not then download and install the driver as mentioned here: https://github.com/Slamtec/rplidar_sdk
  4. Now again run the command mentioned in 1 and see if the line showing up as described in 2.
  5. If yes, in your terminal, run ```ls /dev/ttyUSB0``` & it will show up something like this ```/dev/ttyUSB0```
  6. Now run ```ls -l /dev | grep ttyUSB``` & it will show up like ```crw-rw---- 1....```
  7. Again run ```sudo chmod 666 /dev/ttyUSB0``` & now you have the admin permission to read and write with this device using the port. 
# RPlidar_ros Download
  1. In your terminal, run ```cd ~/catkin_ws/src``` which will take you to the source folder of catkin workspace.
  2. Again run ```git clone https://github.com/robopeak/rplidar_ros.git```& it will make an instance of the rplidar repository in github.
  3. Run ```cd ..``` to get back to the mother folder which is catkin_ws in your terminal.
  4. Now run ```catkin_make``` which will compile the whole catkin workspace for you.
  5. Then run ```source devel/setup.bash``` to source the environment with your current terminal. Don't close the terminal.
  6. Then in a new terminal, run ```roscore``` to start ros master node.
  7. In the terminal which you sourced the environment, run ```roslaunch rplidar_ros view_rplidar.launch```
  8. Rviz should open up and you can visualize the scan.
# RPLidar Hector SLAM
Using Hector SLAM without odometry data on a ROS system with the RPLidar A1.
  1. In your terminal, run ```cd ~/catkin_ws/src``` 
  2. To clone this repository into your src folder of catkin workspace, run ```git clone https://github.com/ArghyaChatterjee/Hector-SLAM-in-ROS-without-odometry-data-in-Nvidia-Jetson-and-Raspberry-pi.git```
  3. Run ```cd ..``` to get back to the mother folder which is catkin_ws in your terminal. 
  4. Now run ```catkin_make``` to compile your catkin workspace.
  5. Again run ```source /devel/setup.bash``` to source the devel folder of your catkin workspace.
  6. Then in a new terminal, run ```roscore``` to start ros master node.
  7. In another terminal source the environment by running ```source devel/setup.bash``` & run ```roslaunch rplidar_ros rplidar.launch```
  8. In another terminal source the enviroment by running ```source devel/setup.bash``` & run ```roslaunch hector_slam_launch tutorial_ar.launch```
  9. Rviz should open up and you can visualize the Hector mapping.
  


Note: What is changed from the original hector slam repository is described below:

  1. In catkin_ws/src/rplidar_hector_slam/hector_slam/hector_mapping/launch/mapping_default.launch 
the second line is replaced with ```<node pkg="tf" type="static_transform_publisher" name="base_to_laser_broadcaster" args="0 0 0 0 0 0 base_link laser 100" />```
  2. The third line is replaced with ```<arg name="base_frame" default="base_link"/>```
  3. The fourth line is replaced with```<arg name="odom_frame" default="base_link"/>```
  4. In catkin_ws/src/rplidar_hector_slam/hector_slam/hector_slam_launch/launch/tutorial.launch  the third line is replaced with```<param name="/use_sim_time" value="false"/>```
