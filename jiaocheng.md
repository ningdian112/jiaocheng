# Ubuntu20.04 + ros2 galatic + autoware.universe + cuda11.6(cudnn8) + OpenPlanner


## ROS galactic
wget http://fishros.com/install -O fishros && . fishros (option 1>>2>>3>>1)\
  [1]:一键安装(推荐):ROS(支持ROS/ROS2,树莓派Jetson)\
  [2]:不更换继续安装\
  [3]:galactic(ROS2)\
  [1]:galactic(ROS2)桌面版\

### Test ros
source /opt/ros/galactic/setup.bash\
ros2 run demo_nodes_cpp talker

## Autoware.universe
### git
sudo apt-get -y update\
sudo apt-get -y install git

### clone autoware
mkdir autoware_universe \
cd autoware_universe/ \
git clone https://github.com/autowarefoundation/autoware.git -b galactic  

### install dependencies
cd autoware\
./setup-dev-env.sh (without install cuda)

### change the source
mkdir src\
sudo gedit autoware.repos
### add in the line 28
universe/external/open_planner:\
    type: git\
    url: https://github.com/ZATiTech/open_planner.git\
    version: main

### load the code to local
vcs import src < autoware.repos

### install the dependencies for autoware
rosdep update --include-eol-distros \
source /opt/ros/galactic/setup.bash \
rosdep install -y --from-paths src --ignore-src --rosdistro $ROS_DISTRO



