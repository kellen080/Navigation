# Navigation

This code is tested on Ubuntu 18.04 with ROS Melodic.

### Installation

    cd ~/catkin_ws/src
    
    git clone https://github.com/kellen080/Indoor_positioning.git
    
    cd ~/catkin_ws
    
    catkin_make_isolated


## Obstacle Avoidance Navigation

### Main Command

###### Simulation

    $ roslaunch rtabmap_drone_example gazebo.launch

###### Real

    $ roslaunch rtabmap_drone_example slam.launch localization:=true

    $ roslaunch rtabmap_drone_example rviz.launch

    $ rosrun rtabmap_drone_example offboard

### Image Transport

#### Simulation

    $ rosrun image_transport republish compressed in:=/r200/camera/color/image_raw raw out:=/image/color/image_raw
    
    $ rosrun image_transport republish compressedDepth in:=/r200/camera/depth/image_raw raw out:=/image/aligned_depth_to_color/image_raw
    
#### Real

    $ rosrun image_transport republish compressed in:=/camera/color/image_raw raw out:=/image/color/image_raw
    
    $ rosrun image_transport republish compressedDepth in:=/camera/aligned_depth_to_color/image_raw raw out:=/image/aligned_depth_to_color/image_raw

---

### SSH

#### VOXL
    
    $ ssh root@192.168.0.199 (oelinux123)
    $ docker start boring_jones
    $ docker exec -it boring_jones /bin/bash
    $ cd
    $ source my_ros_env.sh
    $ roslaunch mavros px4.launch fcu_url:=udp://127.0.0.1:14551@:14551 tgt_system:=${PX4_SYS_ID}
    
#### UP-Board

    $ ssh rvl@192.168.0.39 (rvl122)
    $ source my_ros_env.sh
    $ roslaunch realsense2_camera rs_camera.launch align_depth:=true
    
---

## RTAB-Map SLAM
  
### Mapping Mode
    
#### With D435

    $ roslaunch rtabmap_ros rtabmap.launch rtabmap_args:="--delete_db_on_start" \
    depth_topic:=/camera/aligned_depth_to_color/image_raw \
    rgb_topic:=/camera/color/image_raw \
    camera_info_topic:=/camera/color/camera_info \
    approx_sync:=false
    
#### With D435 and Image Transport

    $ roslaunch rtabmap_ros rtabmap.launch rtabmap_args:="--delete_db_on_start" \
    depth_topic:=/image/aligned_depth_to_color/image_raw \
    rgb_topic:=/image/color/image_raw \
    camera_info_topic:=/camera/color/camera_info \
    approx_sync:=false
    
### Localization Mode

#### With D435

    $ roslaunch rtabmap_ros rtabmap.launch localization:=true \
    depth_topic:=/camera/aligned_depth_to_color/image_raw \
    rgb_topic:=/camera/color/image_raw \
    camera_info_topic:=/camera/color/camera_info \
    approx_sync:=false
    
#### With D435 and Image Transport
    
    $ roslaunch rtabmap_ros rtabmap.launch localization:=true \
    depth_topic:=/image/aligned_depth_to_color/image_raw \
    rgb_topic:=/image/color/image_raw \
    camera_info_topic:=/camera/color/camera_info \
    approx_sync:=false

### Launch RealSense D435

    $ roslaunch realsense2_camera rs_camera.launch  align_depth:=true
    
---
