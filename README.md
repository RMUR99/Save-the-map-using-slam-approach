Task 4 Save the map using SLAM approach 
1)	First find the manual from turtlebot3 
https://emanual.robotis.com/docs/en/platform/turtlebot3/overview/
2)	Press on the PC set up and choose the type mine is (Melodic) 
-	Install ROS on the Remote PC 
$ sudo apt update
$ sudo apt upgrade
$ wget https://raw.githubusercontent.com/ROBOTIS-GIT/robotis_tools/master/install_ros_melodic.sh
$ chmod 755 ./install_ros_melodic.sh 
$ bash ./install_ros_melodic.sh
-	Install dependent ROS packages 
$ sudo apt-get install ros-melodic-joy ros-melodic-teleop-twist-joy \
  ros-melodic-teleop-twist-keyboard ros-melodic-laser-proc \
  ros-melodic-rgbd-launch ros-melodic-depthimage-to-laserscan \
  ros-melodic-rosserial-arduino ros-melodic-rosserial-python \
  ros-melodic-rosserial-server ros-melodic-rosserial-client \
  ros-melodic-rosserial-msgs ros-melodic-amcl ros-melodic-map-server \
  ros-melodic-move-base ros-melodic-urdf ros-melodic-xacro \
  ros-melodic-compressed-image-transport ros-melodic-rqt* \
  ros-melodic-gmapping ros-melodic-navigation ros-melodic-interactive-markers

-	Install TurtleBot3 packages 
$ sudo apt-get install ros-melodic-dynamixel-sdk
$ sudo apt-get install ros-melodic-turtlebot3-msgs
$ sudo apt-get install ros-melodic-turtlebot3

-	Set a name for the TurtleBot3
Choose either burger or waffle mine is burger and below is the command 
echo "export TURTLEBOT3_MODEL=burger" >> ~/.bashrc

-	connect PC to wifi and check the IP address
$ ifconfig


-	Update the ROS IP address With the command below 
$ nano ~/.bashrc


-	Source the bash with the command below
$ source ~/.bashrc

3)	Go to the gazebo simulation and choose the type ( mine is melodic ) 
-	Install the simulation package 
$ cd ~/catkin_ws/src/
 $ git clone -b melodic-devel https://github.com/ROBOTIS-GIT/turtlebot3_simulations.git
$ cd ~/catkin_ws && catkin_make

-	Launch the simulation world 
Since I have chosen burger these are my commands 
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_gazebo turtlebot3_empty_world.launch

-	Operate turtlebot3
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

4)	Go to the SLAM simulation 
-	Launch simulation world 
Choose the type you have (Mine is melodic)
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_gazebo turtlebot3_world.launch

-	Run SLAM node 
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=gmapping

-	Run the teleportation Node 
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch

 Control Your TurtleBot3!
 ---------------------------
 Moving around:
        w
   a    s    d
        x

 w/x : increase/decrease linear velocity
 a/d : increase/decrease angular velocity
 space key, s : force stop

 CTRL-C to quit

-	Save map 
rosrun map_server map_saver -f ~/map

5)	Go to Navigation nodes 
-	Run navigation nodes
 $ roscore

-	Launch the navigation 
$ export TURTLEBOT3_MODEL=burger
$ roslaunch turtlebot3_navigation turtlebot3_navigation.launch map_file:=$HOME/map.yaml
# Save-the-map-using-slam-approach
