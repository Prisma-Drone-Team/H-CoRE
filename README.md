# H-CoRE

This repository contains tools and configurations for H-CoRE (Heterogeneous Cooperative multi-Robot Execution) framework simulation and hardware deployment integrated with ROS2 Humble in Docker environments.

## Article
The description of the single agents' architecture, the software integration, and the framework validation is described in the following article:

Simone D’Angelo*, Francesca Pagano, Riccardo Caccavale, Vincenzo Scognamiglio, Alessandro De Crescenzo, Pasquale Merone, Stefano Ciaravino, Alberto Finzi, and Vincenzo Lippiello, "H-CoRE: A Cooperative Framework for Heterogeneous Multi-Robot Exploration and Inspection"

This work is actually submitted and under review at MDPI - Drones 

## Video
Supplementary video showcasing the proposed framework and the corresponding experimental validation is available at: https://youtu.be/VcLkpbIYOPw

## Architecture Overview

The system consists of several modular ROS2 packages divided into agent-specific Docker environments:

### GCS 
https://github.com/Prisma-Drone-Team/leonardo_managers

### UAV agent
https://github.com/Prisma-Drone-Team/uav_motion_stack.git

### UGV agent

https://github.com/Prisma-Drone-Team/Rover-Navigation.git

### PTZ camera agent

https://github.com/Prisma-Drone-Team/ptz_docker_sw

## Tutorials
H-CoRE framework is fully open-source and available both in plug-and-play simulation and ready to be deployed on actual hardware. 

Tutorials to set up H-CoRE are available at: tutorials/sitl_setup.md 
