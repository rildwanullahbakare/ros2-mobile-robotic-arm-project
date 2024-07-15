# Design Details

## Mobile Base Specifications

The mobile base is the foundation of our robot. Here's a breakdown of its components and properties:

### Base Link

- **Shape**: Box
- **Dimensions**: 0.6 meters (length) x 0.4 meters (width) x 0.2 meters (height)
- **Color**: Blue
- **Mass**: 5.0 kg

### Wheels

The mobile base has two main wheels and one caster wheel.

#### Main Wheels (Left and Right)

- **Shape**: Cylinder
- **Radius**: 0.1 meters
- **Length**: 0.05 meters
- **Color**: Grey
- **Mass**: 1.0 kg each

#### Caster Wheel

- **Shape**: Sphere
- **Radius**: 0.05 meters
- **Color**: Grey
- **Mass**: 0.5 kg

### Joints

#### Base Joint

- **Type**: Fixed
- **Parent Link**: Base Footprint
- **Child Link**: Base Link
- **Origin**: Positioned at (0, 0, 0.1)

#### Wheel Joints

- **Type**: Continuous
- **Parent Link**: Base Link
- **Child Link**: Right/Left Wheel Link
- **Origin**: 
  - Right Wheel: Positioned at (-0.15, -0.225, 0)
  - Left Wheel: Positioned at (-0.15, 0.225, 0)
- **Axis**: Rotation along the Y-axis

#### Caster Wheel Joint

- **Type**: Fixed
- **Parent Link**: Base Link
- **Child Link**: Caster Wheel Link
- **Origin**: Positioned at (0.2, 0, -0.05)

### Gazebo Plugins

#### Differential Drive Controller

- **Plugin Name**: `diff_drive_controller`
- **Filename**: `libgazebo_ros_diff_drive.so`
- **Update Rate**: 50 Hz
- **Wheels**:
  - Left Joint: `base_left_wheel_joint`
  - Right Joint: `base_right_wheel_joint`
- **Kinematics**:
  - Wheel Separation: 0.45 meters
  - Wheel Diameter: 0.2 meters
- **Output**:
  - Publish Odometry: True
  - Publish Odometry TF: True
  - Publish Wheel TF: True
  - Odometry Topic: `odom`
  - Odometry Frame: `odom`
  - Robot Base Frame: `base_footprint`
 
To test the `diff_drive_controller` plugin, use the following command:

```sh
ros2 topic pub -1 /cmd_vel geometry_msgs/msg/Twist "{linear: {x: 0.2}, angular: {z: 0.0}}"
```
## Camera Specifications

A camera sensor has been added to the mobile base to provide visual feedback. The camera is mounted on a fixed joint on the base and includes both visual and collision properties.

### Camera Link

- **Shape**: Box
- **Dimensions**: 0.01 meters (length) x 0.1 meters (width) x 0.05 meters (height)
- **Color**: Grey
- **Mass**: 0.1 kg

### Camera Joints

#### Base to Camera Joint

- **Type**: Fixed
- **Parent Link**: Base Link
- **Child Link**: Camera Link
- **Origin**: Positioned at (0.305, 0, 0.1)

#### Camera Optical Joint

- **Type**: Fixed
- **Parent Link**: Camera Link
- **Child Link**: Camera Optical Link
- **Origin**: Positioned at (0, 0, 0), with rotations of (-π/2, 0, -π/2)

### Gazebo Camera Plugin

- **Reference Link**: Camera Link
- **Material**: Gazebo/Red
- **Sensor Type**: Camera
- **Pose**: Positioned at (0, 0, 0)
- **Visualize**: True
- **Update Rate**: 10.0 Hz
- **Plugin Name**: `camera_controller`
- **Filename**: `libgazebo_ros_camera.so`
- **Frame Name**: `camera_link_optical`


## Robotic Arm Specifications

The robotic arm consists of three main parts: the base link, the forearm link, and the hand link.

### Base Link

- **Shape**: Box
- **Dimensions**: 0.1 meters (length) x 0.1 meters (width) x 0.02 meters (height)
- **Color**: Orange
- **Mass**: 0.5 kg

### Forearm Link

- **Shape**: Cylinder
- **Radius**: 0.02 meters
- **Length**: 0.3 meters
- **Color**: Yellow
- **Mass**: 0.3 kg

### Hand Link

- **Shape**: Cylinder
- **Radius**: 0.02 meters
- **Length**: 0.3 meters
- **Color**: Orange
- **Mass**: 0.3 kg

### Joints

#### Base to Forearm Joint

- **Type**: Revolute
- **Movement Range**: 0 to 90 degrees
- **Effort**: 100
- **Velocity**: 100
- **Friction**: 0.05
- **Damping**: 0.1

#### Forearm to Hand Joint

- **Type**: Revolute
- **Movement Range**: 0 to 90 degrees
- **Effort**: 100
- **Velocity**: 100
- **Friction**: 0.05
- **Damping**: 0.1

### Gazebo Plugins

#### Joint State Publisher

- **Update Rate**: 10 Hz
- **Joint Names**: All joints in the arm

#### Joint Pose Trajectory

- **Update Rate**: 2 Hz

To test the `joint_pose_trajectory` plugin, use the following command:

```sh
ros2 topic pub -1 /set_joint_trajectory trajectory_msgs/msg/JointTrajectory '{header: {frame_id: arm_base_link}, joint_names: [arm_base_forearm_joint, forearm_hand_joint], points: [{positions: [0.0, 0.0]}]}'
