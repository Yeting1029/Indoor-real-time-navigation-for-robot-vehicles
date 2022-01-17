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
$ roslaunch rplidar_ros rplidar.launch  
$ rostopic list  
$ rostopic echo /scan
