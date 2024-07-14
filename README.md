# ROS2 Robotic Arm Project

Welcome to my ROS2 Mobile Robotic Arm Project! This project covers designing custom robot with ROS2 URDF (Unified Robot Description Format), visualizing the robot and its TF (Transform) on RVIZ2 and simulating it in Gazebo. The main goal here is to firstly create a mobile base and enhancing the mobile base by adding a camera on a fixed joint on the base  and a simple 2-axis robotic arm on top of it. This project is to prepare for more advanced robotic arm control in the future.

## Project Overview

In this project, we are building a mobile base with a camera sensor added to provide visual feedback and a basic robotic arm to sits on the base. The movement of the mobile base is enabled by a diff_drive Gazebo plugin and the arm is controlled using another Gazebo plugin, which simulates the robot's movement. Although the arm performs simple movements, this project is about practicing and understanding the core concepts of ROS2, RVIZ2 and Gazebo.

## Features

- **URDF Models**: Detailed descriptions of the robotic arm and mobile base.
- **RVIZ Visualization**: View the mobile base and robotic arm framework and TF.
- **Gazebo Simulation**: Simulate the the mobile base and robotic arm in a virtual environment.
- **Control Scripts**: Basic scripts to control the robotic arm using ROS2 topics.

## What's Inside

Here's a breakdown of what you'll find in this project:

- `launch/`: Contains launch files to start the simulation.
- `urdf/`: Holds all the URDF and xacro files describing the robot.
- `config/`: Configuration files for Gazebo plugins.
- `images/`: Project images, including the frame diagram.
- `scripts/`: Python scripts for controlling the robotic arm.
- `worlds/`: Gazebo world files where the robot operates.
- `rviz/`: Configuration files for RViz, a visualization tool.

## Getting Started

### Prerequisites

To run this project, you need:
- ROS2 Humble installed on your system.
- Gazebo and RViz installed.

### How to Run the Simulation

1. **Clone the Repository**:
   ```sh
   git clone https://github.com/Realone16/ros2-mobile-robotic-arm-project.git
   cd ros2-mobile-robotic-arm-project
