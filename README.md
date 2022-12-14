# Turtlebot3-burger-backup

|OS|Type|
|--|--|
|OS|Ubuntu 20.04 LTS|
|ROS|Noetic|

## ~/.bashrc

```bash
# bashrc aliases
alias gb='gedit ~/.bashrc'
alias sb='source ~/.bashrc'
alias cb='cat ~/.bashrc'

# ROS aliases
alias cw='cd ~/catkin_ws'
alias cs='cd ~/catkin_ws/src'
alias cm='cd ~/catkin_ws && catkin_make'

# ROS setting
source /opt/ros/noetic/setup.bash

# ROS Network
export ROS_IP=192.168.0.4
export ROS_MASTER_URI=http://${ROS_IP}:11311
export ROS_HOSTNAME=${ROS_IP}

export TB3_MODEL=burger
export TURTLEBOT3_MODEL=${TB3_MODEL}

# Cartographer
# Cartographer aliases
alias ccw='cd ~/carto_ws'
alias ccs='cd ~/carto_ws/src'
alias ccm='cd ~/carto_ws && catkin_make_isolated --install --use-ninja'

source ~/carto_ws/install_isolated/setup.bash	# Cartographer
```

## Connect
### In master PC
```
ssh ubuntu@192.168.0.200
```
```
roslaunch turtlebot3_bringup turtlebot3_robot.launch
```
#### Teleop
```
roslaunch turtlebot3_teleop turtlebot3_teleop_key.launch
```

### In Raspberry pi 4
#### OpenCR Update
```
sudo dpkg --add-architecture armhf
sudo apt-get update
sudo apt-get install libc6:armhf

export OPENCR_PORT=/dev/ttyACM0
export OPENCR_MODEL=burger_noetic
rm -rf ./opencr_update.tar.bz2

wget https://github.com/ROBOTIS-GIT/OpenCR-Binaries/raw/master/turtlebot3/ROS1/latest/opencr_update.tar.bz2 
tar -xvf opencr_update.tar.bz2 

cd ./opencr_update
./update.sh $OPENCR_PORT $OPENCR_MODEL.opencr
```
## Cartographer in Master PC
https://github.com/cartographer-project/cartographer_ros/issues/1726
```
sudo apt update
sudo apt install -y python3-wstool python3-rosdep ninja-build stow
cd ~/carto_ws/
wstool init src
wstool merge -t src https://raw.githubusercontent.com/cartographer-project/cartographer_ros/master/cartographer_ros.rosinstall
wstool update -t src
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src --rosdistro=noetic -y
src/cartographer/scripts/install_abseil.sh
sudo apt remove ros-noetic-abseil-cpp # Ignore it if it doesn't work.
catkin_make_isolated --install --use-ninja
```
```
source ~/carto_ws/install_isolated/setup.bash
roslaunch turtlebot3_slam turtlebot3_slam.launch slam_methods:=cartographer
```

## Reference
[ROBOTIS:Quick Start Guide](https://emanual.robotis.com/docs/en/platform/turtlebot3/quick-start/)<br>
https://github.com/msjun23/bashrc-backup
