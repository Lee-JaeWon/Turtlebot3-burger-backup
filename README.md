# Turtlebot3-burger-backup

|||
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
export ROS_IP=192.168.0.4 # Master PC
export ROS_MASTER_URI=http://${ROS_IP}:11311
export ROS_HOSTNAME=${ROS_IP}

export TB3_MODEL=burger
export TURTLEBOT3_MODEL=${TB3_MODEL}
```

## Turtlebot3(Raspberry pi 4)
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
export ROS_IP=192.168.0.200
export ROS_MASTER_URI=http://192.169.0.4:11311
export ROS_HOSTNAME=${ROS_IP}

export TB3_MODEL=burger
export TURTLEBOT3_MODEL=${TB3_MODEL}
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
