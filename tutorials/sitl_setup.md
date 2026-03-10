# H-CoRE Simulation Setup Tutorial

This tutorial provides comprehensive instructions for setting up and running the H-CoRE (Heterogeneous Cooperative multi-Robot Execution) framework simulation environment. The system enables simulation of heterogeneous robotic agents including UAVs (Unmanned Aerial Vehicles), UGVs (Unmanned Ground Vehicles) and PTZ (Pan-Tilt-Zoom Camera) in both single-agent and multi-agent configurations.

<div align="center">
<img src="../figs/h-core_simu.png" alt="H-CoRE Multi-Robot Simulation" width="70%">
</div>

*Figure 1: H-CoRE Framework simulation showing cooperative UAV and UGV agents in Gazebo Garden environment*

## Architecture Overview

The H-CoRE framework implements a modular architecture with dockerized environments for each agent type, enabling seamless integration and isolated development:

### System Components

- **UAV Agent**: PX4 SITL-based drone simulation with autonomous navigation
- **UGV Agent**: Ground robot with advanced navigation and exploration capabilities  
- **Ground Control Station (GCS)**: Mission management and monitoring interface
- **PTZ Camera Agent**: Pan-tilt-zoom camera system for surveillance tasks

### Software Stack

- **ROS2 Humble**: Primary robotics framework
- **Gazebo Garden**: 3D physics simulation environment
- **PX4 v1.14+**: Autopilot firmware for UAV control
- **Navigation2**: Advanced navigation stack for UGV operations
- **Docker**: Containerized deployment environments

### Communication Architecture

All agents communicate through the ROS2 DDS middleware using domain ID 17 for simulation environments. The system utilizes headless simulation for optimal real-time performance, with RViz providing comprehensive visualization capabilities.

## System Requirements

### Hardware Requirements
- **CPU**: Intel i5-8th generation or equivalent AMD processor
- **RAM**: Minimum 8 GB, recommended 16 GB
- **GPU**: NVIDIA GPU with CUDA support (optional but recommended)
- **Storage**: 20 GB free disk space

### Software Dependencies
- **Ubuntu 22.04 LTS** (Jammy Jellyfish)
- **Docker Engine** (version 20.10+)
- **Docker Compose** (version 2.0+)
- **Git** with LFS support
- **X11** forwarding capability for visualization

## Installation and Setup

### 1. Repository Preparation

Clone the H-CoRE simulation repositories to your development workspace:

```bash
# Clone H-CoRE main repository
git clone https://github.com/Prisma-Drone-Team/H-CoRE.git && cd H-CoRE

# Clone UAV motion stack with SITL utilities
git clone --recursive https://github.com/Prisma-Drone-Team/uav_motion_stack.git -b paper_stable sitl_utils

# Clone UGV simulation stack
git clone https://github.com/Prisma-Drone-Team/rover_sim_motion_stack.git

# Clone PTZ simulation stack
git clone --recursive https://github.com/Prisma-Drone-Team/ptz_docker_sw.git
```

### 2. UAV Simulation Environment Setup

Navigate to the UAV simulation directory and configure the environment:

```bash
cd ~/H-CoRE/sitl_utils

# Clone PX4 Neabotics custom firmware (required for plug-and-play functionality)
git clone --single-branch -b feature/diffgains_fix_servo_k \
    https://github.com/Prisma-Drone-Team/Px4_hcore_autopilot.git PX4_neabotics --recursive

# Build UAV Docker image
cd docker
docker build -t leo-img -f px4_humble_dockerfile.txt .
```

### 3. UGV Simulation Environment Setup

Configure the ground vehicle simulation stack:

```bash
cd ~/H-CoRE/rover_sim_motion_stack

# Select appropriate branch based on simulation requirements
# For standalone UGV simulation:
git checkout leonardo

# For multi-robot simulation:
git checkout multi-robot

# Build UGV Docker image
./docker_build.sh rover_sim_image
```
### 4. PTZ Simulation Environment Setup
```bash
cd ~/H-CoRE/rover_sim_motion_stack

# Select appropriate branch based on simulation requirements
# For standalone UGV simulation:
git checkout paper

# For multi-robot simulation:
git checkout simulation

# Build UGV Docker image
./docker_build.sh

```

### 5. Environment Configuration

Enable X11 forwarding for GUI applications:

```bash
# Allow Docker containers to access X11 display
xhost +local:docker

# Configure display variable (if needed)
export DISPLAY=:0
```

## Single Agent Simulation

### UAV (Drone) Single Agent Simulation

The UAV simulation provides a complete PX4 SITL environment with autonomous navigation capabilities.

#### Starting the UAV Simulation

```bash
cd ~/H-CoRE/sitl_utils

# Launch UAV simulation container
./run_cnt.sh
```

Within the container, the simulation environment is automatically configured. To start the simulation:

```bash
# Start the UAV simulation using TMUX session management
tmuxp load src/pkg/babyk_drone_manager/utils/simulation.yml
```

#### UAV Simulation Components

The TMUX session launches multiple components:

- **PX4 SITL**: Core autopilot simulation with Gazebo Garden integration
- **RViz**: 3D visualization interface with pre-configured drone perspective
- **ArUco Detector**: Computer vision node for marker-based localization  
- **MicroXRCE Agent**: Communication bridge between PX4 and ROS2
- **ROS-Gazebo Bridge**: Sensor data and odometry relay services

#### UAV Control Interface

The drone can be controlled through multiple interfaces:

- **Joy Controller**: Gamepad-based manual control
- **Mission Planner**: Waypoint-based autonomous navigation
- **Teleoperation**: Keyboard and mouse control via dedicated ROS2 nodes

### UGV (Rover) Single Agent Simulation

The UGV simulation implements advanced autonomous navigation using the Navigation2 stack.

#### Starting the UGV Simulation

```bash
cd ~/H-CoRE/rover_sim_motion_stack

# Launch UGV simulation with automatic initialization
./docker_run.sh rover_sim_image rover_container
```

# Within the container, launch the rover simulation
```bash
ros2 launch rover_bringup rover_sim.launch
```

#### UGV Simulation Features

The rover simulation includes:

- **Autonomous Navigation**: Advanced path planning with obstacle avoidance
- **SLAM Capabilities**: Simultaneous localization and mapping using multiple sensors
- **Object Detection**: YOLOv11-based perception system
- **Exploration Algorithms**: Coverage path planning for area exploration
- **Multi-Sensor Fusion**: LiDAR and camera data integration

#### UGV Navigation Interface

Navigate the rover using:

- **Goal Setting**: Interactive marker placement in RViz
- **Exploration Mode**: Autonomous area coverage algorithms
- **Manual Control**: Direct velocity commands via teleoperation nodes

### PTZ (Pan-Tilt-Zoom) Camera Single-robot Simulation

The PTZ camera simulation provides high-precision surveillance capabilities with full 3-DOF control and real-time zoom functionality.

#### Starting the PTZ Simulation

```bash
cd H-CoRE/ptz_docker_sw

# Run Docker container without GPU
./docker_run.sh

# Run Docker container with GPU
./docker_run_gpu.sh 

# Launch complete simulation environment including PTZ camera
ros2 launch ptz_gz launch_sim.launch
```

The PTZ camera is automatically spawned in the Leonardo race environment waiting for a task. e.g.:

 ```bash
  ros2 topic pub --once /seed_pdt_camera/command std_msgs/msg/String "data: cover((1,0),(5,0),(5,3),(1,3),34,2,0:10:00)"


  ros2 topic pub --once /seed_pdt_camera/command std_msgs/msg/String "data: watchto(goal2)"
```

#### PTZ Camera System Features

The PTZ simulation includes:

- **3-DOF Control**: Full pan, tilt, and zoom axis control with configurable limits
- **Real-time Zoom**: CameraZoomPlugin with 1x to 125x magnification range  
- **Dual Control Modes**: Position absolute and velocity-based control
- **Visual Feedback**: Real-time camera view with field-of-view adjustment
- **Hardware Integration**: Compatible with motion stack architecture for real PTZ systems

#### PTZ Technical Specifications

- **Pan Range**: ±170° with precision control
- **Tilt Range**: ±90° vertical movement  
- **Zoom Range**: 1x to 125x optical magnification
- **Control Frequency**: 20Hz position updates for smooth motion
- **Camera Resolution**: 1920x1080 HD video stream at 25 FPS

## Multi-Robot Simulation

The multi-robot configuration enables cooperative behavior between UAV and UGV agents, demonstrating the full H-CoRE framework capabilities.

### Multi-Robot System Architecture

The multi-robot simulation establishes communication between heterogeneous agents through shared ROS2 domain configuration, enabling:

- **Collaborative Mission Planning**: Distributed task allocation between agents
- **Shared Situational Awareness**: Common world representation across all agents
- **Cooperative Navigation**: Coordinated movement planning to avoid conflicts
- **Data Fusion**: Integration of sensor data from multiple perspectives

### Starting Multi-Robot Simulation

The multi-robot simulation requires coordinated launch of both UAV and UGV containers to establish the shared simulation environment.

#### Step 1: Launch Multi-Robot UAV Container

```bash
cd ~/H-CoRE/sitl_utils

# Start UAV container with multi-robot configuration
./run_multi_cnt.sh
```

#### Step 2: Initialize UAV Multi-Robot Session

Within the UAV container, launch the multi-robot session which includes Gazebo world initialization:

```bash
# Launch multi-robot simulation session (includes Gazebo world setup)
tmuxp load src/pkg/babyk_drone_manager/utils/multi_simulation.yml
```

This TMUX session establishes the shared Gazebo Garden environment that the three agents will operate in.

#### Step 3: Launch UGV Container

In a separate terminal, launch the UGV container in multi-robot configuration:

```bash
cd ~/H-CoRE/rover_sim_motion_stack

# Ensure you're on the multi-robot branch
git checkout multi-robot

# Launch UGV container with multi-robot configuration
./docker_run.sh rover_sim_image rover_multi_container
```

#### Step 4: Initialize UGV Navigation Stack

Within the UGV container, launch the rover navigation and control stack:

```bash
# Start the UGV navigation stack for multi-robot operation
ros2 launch rover_bringup rover_sim.launch
```
#### Step 5: Launch PTZ Container
```bash
cd ~/H-CoRE/ptz_docker_sw

# Ensure you're on the multi-robot branch
git checkout simulation

# Launch UGV container with multi-robot configuration
./docker_run.sh

export ROS_DOMAIN_ID=17
ros2 launch ptz_manager ptz_navigation_stack.launch.py
```

#### Step 5: Verify Multi-Robot Communication

Confirm that both agents are communicating through the shared ROS2 domain:

```bash
# Check active nodes from both agents
ros2 node list

# Verify topic communication between agents
ros2 topic list | grep -E "(uav|ugv)"
```

### Multi-Robot Coordination Features

The multi-robot simulation demonstrates:

- **Shared Gazebo World**: Both agents operate in the same physics simulation
- **Unified Coordinate System**: Common reference frame for all operations
- **Inter-Agent Communication**: ROS2 topic sharing for coordination messages
- **Distributed Perception**: Complementary sensor coverage between aerial and ground perspectives

### Mission Coordination Scenarios

Test various cooperative scenarios:

1. **Search and Rescue**: UAV provides aerial reconnaissance while UGV performs ground navigation
2. **Infrastructure Inspection**: Coordinated inspection with different viewpoints
3. **Area Mapping**: Combined aerial and ground SLAM for comprehensive mapping
4. **Target Tracking**: Cooperative target following with handoff capabilities

## Visualization with RViz

RViz provides comprehensive visualization for both single-agent and multi-robot simulations through optimized headless operation.

### RViz Configuration Features

The pre-configured RViz setup includes:

- **3D Environment Visualization**: Real-time Gazebo world representation
- **Robot State Display**: Joint states, transforms, and motion trajectories  
- **Sensor Data Overlay**: LiDAR, camera, and depth sensor visualization
- **Navigation Visualization**: Path planning, costmaps, and goal markers
- **Multi-Agent Tracking**: Simultaneous display of all active agents

### Custom RViz Perspectives

Access specialized visualization modes:

```bash
# UAV-focused perspective
ros2 run rviz2 rviz2 -d ~/ros2_ws/src/pkg/babyk_drone_manager/rviz/leo.rviz

# Navigation-focused perspective  
ros2 run rviz2 rviz2 -d ~/rover_ws/src/pkg/rover_manager/rover.rviz
```
### Performance Optimization

The headless simulation configuration ensures optimal performance:

- **GPU Acceleration**: Automatically detected CUDA support for enhanced rendering
- **Resource Management**: Efficient CPU and memory usage through containerization
- **Real-Time Constraints**: Low-latency communication for responsive control
- **Scalable Architecture**: Support for additional agents with minimal performance impact

## Conclusion

This tutorial provides a comprehensive foundation for operating the H-CoRE simulation environment in both single-agent and multi-robot configurations. The dockerized architecture ensures reproducible deployment while the headless operation with RViz visualization maintains optimal performance for complex cooperative robotics research and development.

For additional resources and advanced configuration options, refer to the individual repository documentation and the H-CoRE framework research publication.

## Support and Contributions
For technical support and bug reports:

- **H-CoRE Framework Issues**: [H-CoRE Repository Issues](https://github.com/Prisma-Drone-Team/H-CoRE/issues)
- **UAV Motion Stack Issues**: [UAV Motion Stack Issues](https://github.com/Prisma-Drone-Team/uav_motion_stack/issues)
- **UGV Simulation Stack Issues**: [Rover Sim Motion Stack Issues](https://github.com/Prisma-Drone-Team/rover_sim_motion_stack/issues)

For comprehensive documentation, refer to the H-CoRE framework research publication (currently under review).
