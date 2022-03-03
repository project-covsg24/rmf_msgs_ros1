# rmf_msgs_ros1
RMF message definitions for bridging ROS2 and ROS1

## Setup
TESTED ON: ROS1 Noetic + ROS2 Foxy

Clone this package to your ROS1 workspace and build it:
```bash
cd <your_ros1_catkin_ws>/src
git clone https://github.com/project-covsg24/rmf_msgs_ros1
cd ..
catkin build
```

Clone the modified RMF messages package, which has the ROS bridge message mappings, to your ROS2 workspace:
```bash
cd <your_ros2_colcon_ws>/src
git clone https://github.com/project-covsg24/rmf_internal_msgs
cd ..
colcon build
```

Clone the ros1_bridge to your ROS2 workspace and build the ros1_bridge
```bash
cd <your_ros2_colcon_ws>/src
git clone https://github.com/ros2/ros1_bridge
cd ..

# Source both ROS1 and ROS2 workspaces, so that the bridge can be compiled
source /opt/ros/noetic/setup.bash
source /opt/ros/foxy/setup.bash
source <your_ros1_catkin_ws>/devel/setup.bash
source <your_ros2_colcon_ws>/install/setup.bash

# This will take some time
colcon build --symlink-install --cmake-force-configure
```

Check if the bridge is built correctly by listing the connections via:
```bash
ros2 run ros1_bridge dynamic_bridge --print-pairs | grep rmf
```

You should see something similar:
```bash
$ ros2 run ros1_bridge dynamic_bridge --print-pairs | grep disp
  - 'rmf_dispenser_msgs/msg/DispenserRequest' (ROS 2) <=> 'rmf_dispenser_msgs_ros1/DispenserRequest' (ROS 1)
  - 'rmf_dispenser_msgs/msg/DispenserRequestItem' (ROS 2) <=> 'rmf_dispenser_msgs_ros1/DispenserRequestItem' (ROS 1)
  - 'rmf_dispenser_msgs/msg/DispenserResult' (ROS 2) <=> 'rmf_dispenser_msgs_ros1/DispenserResult' (ROS 1)
  - 'rmf_dispenser_msgs/msg/DispenserState' (ROS 2) <=> 'rmf_dispenser_msgs_ros1/DispenserState' (ROS 1)
  
  ...
```
