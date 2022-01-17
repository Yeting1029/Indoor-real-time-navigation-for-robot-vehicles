# Indoor-real-time-navigation-for-robot-vehicles
Final year project for the Embedded Systems Minor

GSE5 - SUN Yeting - YU Bicong
## ROS setup and installation
$ sudo apt-get update  
$ sudo apt install ros-melodic-desktop-full  
## Environment setup
$ echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc  
$ echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc  
$ source ~/.bashrc  
##  Create and build a catkin workspace
$ mkdir -p ~/catkin_ws/src  
$ cd ~/catkin_ws/  
$ catkin_make  
## Detect the lidar connect normally
$ ls -l /dev | grep ttyUSB  
$ sudo chmod 666 /dev/ttyUSB0  
## Test the lidar
### Show the data of lidar in the terminal
$ roslaunch rplidar_ros rplidar.launch  
$ rostopic list  
$ rostopic echo /scan
### Show the data of lidar in rviz
$ rviz  
Change the Fixed Frame to laser, and add LaserScan.  
Set the LaserScan topic to /scan.  
## Build a map by using Lidar
### Scan the environment
Use Hector-SLAM Package.  
$ roslaunch rplidar_ros rplidar.launch  
$ roslaunch hector_slam_launch tutorial.launch  
Then we can move the lidar slowly, and observe the map.  
### Save the map
$ rosrun map_server map_saver -f my_map  
## Autonomous navigation with ROS
$ export TURLEBOT3_MODEL = burger  
$ roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch  
$ roslaunch turtlebot3_navigation turtlebot_navigation.launch map_file:=$HOME/map.yaml  
