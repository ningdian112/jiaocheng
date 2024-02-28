## Ubuntu20.04 + ros2 galatic + autoware.universe + cuda11.6(cudnn8)


# ROS galactic
wget http://fishros.com/install -O fishros && . fishros (option 1>>2>>1>>1)
Test ros
source /opt/ros/galactic/setup.bash
ros2 run demo_nodes_cpp talker

# Autoware.universe
#git
sudo apt-get -y update
sudo apt-get -y install git

# clone autoware
mkdir autoware_universe
cd autoware_universe/
git clone https://github.com/autowarefoundation/autoware.git -b galactic

# install dependencies
cd autoware
./setup-dev-env.sh (without install cuda)

# change the source
mkdir src
sudo gedit autoware.repos
# add in the line 28
universe/external/open_planner:
    type: git
    url: https://github.com/ZATiTech/open_planner.git
    version: main

# load the code to local
vcs import src < autoware.repos
