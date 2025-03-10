# pepper_virtual_noetic
This repo is an updated version of [pepper_virtual](https://github.com/awesomebytes/pepper_virtual) for ROS Noetic

## Dependencies:

To run you need another package in your workspace:

# MODIFIED VERSION that works (at least on Noetic in 16/02/2025)

For this modified version (differs from the origin upstream) you'll also need:
- [https://github.com/awesomebytes/gazebo_model_velocity_plugin](https://github.com/awesomebytes/gazebo_model_velocity_plugin)
- Sensor msgs
- [pepper_robot_noetic](https://github.com/dcuevasa/pepper_robot_noetic)


# Installation
This should get your workspace up and running:
```bash
mkdir -p pepper_sim_ws/src
cd pepper_sim_ws/src
git clone https://github.com/dcuevasa/pepper_robot_noetic
git clone https://github.com/dcuevasa/pepper_virtual_noetic.git
git clone https://github.com/dcuevasa/gazebo_model_velocity_plugin_noetic
# In case you are missing any of these
sudo apt-get install ros-noetic-tf2-sensor-msgs ros-noetic-ros-control ros-noetic-ros-controllers ros-noetic-gazebo-ros ros-noetic-gazebo-ros-control ros-noetic-gazebo-plugins ros-noetic-controller-manager ros-noetic-ddynamic-reconfigure-python
cd ..
catkin_make
source devel/setup.bash
# Launch your preferred simulation here
roslaunch pepper_gazebo_plugin pepper_gazebo_plugin_in_office_CPU.launch

# (On another shell that you sourced the workspace) Check stuff on Rviz
rosrun rviz rviz -d `rospack find pepper_gazebo_plugin`/config/pepper_sensors.rviz
```

**I removed the /pepper Namespace from .xacro files modified in the latest commit (when writing this Readme.md)**
You'll find `/cmd_vel` to command the base, for example, using `rosrun rqt_robot_steering rqt_robot_steering`.

You can also move the joints via the *follow_joint_trajectory* controllers, for example, using `rosrun
rqt_joint_trajectory_controller rqt_joint_trajectory_controller`.

If you want to simulate the RGB cameras with different resolutions you must go to `pepper_robot/pepper_description/urdf/pepper1.0_generated_urdf/pepperGazebo.xacro` (and/or `pepperGazeboCPU.xacro`) and change the `CameraTop_frame` `<width>640</width>` `<height>480</height>` tags. 

Further documentation on:
- [pepper_virtual](https://github.com/awesomebytes/pepper_virtual)
