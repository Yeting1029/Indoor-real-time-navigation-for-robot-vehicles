# Indoor-real-time-navigation-for-robot-vehicles
Final year project for the Embedded Systems Minor  
GSE5 - SUN Yeting - YU Bicong
## Prerequisite, compile and run
Ubuntu 18.04  
ROS Melodic
## Demonstration video
OpenCR set up and control robot by keyboard: https://youtu.be/CJ8-lHX4I2Q  
Simulate Navigation: https://youtu.be/C8kooJ65Fe0  
Real-time Navigation: https://youtu.be/v8mUfoLE1SI  
## ROS setup and installation
```
$ sudo apt-get update
$ sudo apt install ros-melodic-desktop-full
```
## Environment setup
```
$ echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc  
$ echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc  
$ source ~/.bashrc  
```
##  Create and build a catkin workspace
```
$ mkdir -p ~/catkin_ws/src  
$ cd ~/catkin_ws/  
$ catkin_make  
```
## Detect the lidar connect normally
```
$ ls -l /dev | grep ttyUSB  
$ sudo chmod 666 /dev/ttyUSB0  
```
## Test the lidar
Show the data of lidar in the terminal:
```
$ roslaunch rplidar_ros rplidar.launch  
$ rostopic list  
$ rostopic echo /scan
```
Show the data of lidar in rviz:
```
$ rviz  
```
Change the Fixed Frame to laser, and add LaserScan.  
Set the LaserScan topic to /scan.  
## Build a map by using Lidar
### Scan the environment
Use Hector-SLAM Package.  
```
$ roslaunch rplidar_ros rplidar.launch  
$ roslaunch hector_slam_launch tutorial.launch  
```
Then we can move the lidar slowly, and observe the map.  
### Save the map
```
$ rosrun map_server map_saver -f my_map  
```
## Simulate navigation with ROS
```
$ export TURLEBOT3_MODEL = burger  
$ roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch  
$ roslaunch turtlebot3_navigation turtlebot_navigation.launch map_file:=$HOME/my_map.yaml  
```
## SBC setup
Download Turtlebot3 SBC image: http://www.robotis.com/service/download.php?no=1738  
Use Disks utility to burn the image file to the SD card:
```
Select the microSD card in the left panel.  
Select Restore Disk Image option.  
Open the .img file from local disk.  
Click Start Restoring... > Restore button.  
```
## Configure communication with Turtlebot3
We use hotspots to establish communication.  
Find IP address(Our IP address is 172.20.10.6 and 172.20.10.3):
```
ifconfig
```
Modify the ~./bashrc in Remote PC, write the following to the end of the file:
```
export ROS_MASTER_URI=http://172.20.10.6:11311
export ROS_HOSTNAME=172.20.10.6
```
Modify the ~./bashrc in Turtlebot, write the following to the end of the file:
```
export ROS_MASTER_URI=http://172.20.10.6:11311
export ROS_HOSTNAME=172.20.10.3
```
## Use Turtlebot3 to navigation
Connect to Turtlebot3:
```
$ ssh pi@172.20.10.3  
```
In Remote PC:
```
$ roscore
```
In Turtlebot:
```
$ roslaunch turtlebot3_bringup turtlebot3_robot.launch  
```
In Remote PC:  
Control Turtlebot by the keyboard
```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```
Navigation in rviz
```
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/my_map.yaml
```
