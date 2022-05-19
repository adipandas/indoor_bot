
[GazeboSim]: media/indoor_bot_cartographer_slam_gazebo.gif "Sample of gazebo sim"
[Rviz]: media/indoor_bot_cartographer_slam_rviz.gif "Sample of rviz"
[GazeboSimLocalizationAMCL]: media/indoor_bot_localization_amcl_gazebo.gif "indoor_bot gazebosim localization using AMCL"
[RVizLocalizationAMCL]: media/indoor_bot_localization_amcl_rviz.gif "indoor_bot rviz localization using AMCL"
[GazeboSimAutoSLAM]: media/auto_slam_gazebo.gif "indoor_bot gazebosim localization using AMCL"
[RVizAutoSLAM]: media/auto_slam_rviz.gif "indoor_bot rviz localization using AMCL"

# indoor_bot

``indoor_bot`` is simple differential drive robot for indoor environments simulated using GazeboSim and ROS. Currently, it simulates a 2D-LiDAR sensor, an IMU and a simple camera as gazebo plugins.

This package includes some demos explaining use of this package for SLAM and Localization.

<br>
<br>

# SLAM

GazeboSim |  Cartographer-SLAM
:-------------------------:|:-------------------------:
![GazeboSim][GazeboSim]  |  ![RViz][Rviz]

<br>
<br>

# Autonomous exploration for SLAM

GazeboSim |  Autonomous-SLAM 
:-------------------------:|:-------------------------:
![GazeboSim][GazeboSimAutoSLAM]  |  ![RViz][RVizAutoSLAM]

<br>
<br>

# Localization and Navigation

Gazebo |  Rviz
:-------------------------:|:-------------------------:
 ![GazeboSimLocalizationAMCL][GazeboSimLocalizationAMCL]   |  ![RVizLocalizationAMCL][RVizLocalizationAMCL]

<br>
<br>


# Installation

This package was developed for ROS-melodic. But should be compatible for other versions of ROS1.

1. Install ROS: http://wiki.ros.org/ROS/Installation

2. Install the packages by executing the following commands in your terminal:

    ```bash
    source /opt/ros/melodic/setup.bash

    sudo apt-get install ros-${ROS_DISTRO}-gazebo-*
    sudo apt-get install ros-${ROS_DISTRO}-navigation
    sudo apt-get install ros-${ROS_DISTRO}-joint-state-*
    sudo apt-get install ros-${ROS_DISTRO}-visualization-msgs
    sudo apt-get install ros-${ROS_DISTRO}-cartographer-*
    sudo apt install ros-${ROS_DISTRO}-multirobot-map-merge 
    sudo apt install ros-${ROS_DISTRO}-explore-lite
    sudo apt-get install ros-${ROS_DISTRO}-teleop-twist-keyboard
    ```

3. Clone this repo and build the package.
    ```bash
    source /opt/ros/melodic/setup.bash
    mkdir -p ~/catkin_ws/src
    cd ~/catkin_ws/src

    git clone https://github.com/adipandas/indoor_bot.git
    cd ~/catkin_ws
    catkin_make
    source devel/setup.bash
    ```

# How to use?

### SLAM

Launch SLAM and Map the environment using teleoperation.

```bash
source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bash

roslaunch indoor_bot cartographer_slam_teleop.launch
```

Instead of manually building the map, you may prefer also try to use RRT-exploration to autonomously map the robot frontier. For more documentation, please refer **[this page](http://wiki.ros.org/rrt_exploration)**.

```bash
source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bash

roslaunch indoor_bot cartographer_slam_rrt_exploration.launch
```

Once mapping is complete use map-server to save the map. In onother terminal execute the following to save your map:

```bash
source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bash

roscd indoor_bot
cd maps
rosrun map_server map_saver -f <robotworldname>
```

### Localization and Navigation

To localize using the map generated from SLAM you can use the following command:

```bash
source /opt/ros/melodic/setup.bash
source ~/catkin_ws/devel/setup.bash

roslaunch indoor_bot amcl_localization.launch map_file:=/path/to/map.yaml world_file:=/path/to/your_gazebo.world
```


# References

1. ROS Navigation Stack: [link](http://wiki.ros.org/navigation)
2. RRT exploration: [link](http://wiki.ros.org/rrt_exploration)
3. Cartographer SLAM: [link](https://google-cartographer-ros.readthedocs.io/)
4. teleop_twist_keyboard: [link](http://wiki.ros.org/teleop_twist_keyboard)
