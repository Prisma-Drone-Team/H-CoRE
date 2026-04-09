# H-CoRE

This repository contains tools and configurations for H-CoRE (Heterogeneous Cooperative multi-Robot Execution) framework simulation and hardware deployment integrated with ROS2 Humble in Docker environments.

## Article
The description of the single agents' architecture, the software integration, and the framework validation is described in the following article:

D’Angelo, S., Pagano, F., Caccavale, R., Scognamiglio, V., De Crescenzo, A., Merone, P., Ciaravino, S., Finzi, A., & Lippiello, V. (2026). H-CoRE: A Cooperative Framework for Heterogeneous Multi-Robot Exploration and Inspection. Drones, 10(4), 232. https://doi.org/10.3390/drones10040232

This work is published on the MDPI - Drones journal and is available online as open access. 

## Video
Supplementary video showcasing the proposed framework and the corresponding experimental validation is available at: https://www.youtube.com/watch?v=32JMqU83qIw

## Developers and License

<div align="center">
<img src="figs/logo_prisma.jpg" alt="H-CoRE" width="25%">
</div>

**Developed by**: Aerial Robotics Group - [PRISMA Lab](https://github.com/prisma-lab), University of Naples Federico II

**Lead Developers**:
- Simone D'Angelo (Corresponding author)
- Francesca Pagano  
- Riccardo Caccavale
- Vincenzo Scognamiglio

**License**: This software is **open-source** and freely available for research and educational purposes. 

**Citation**: If you use this framework in your research, please cite the following paper:

```bibtex

@Article{drones10040232,
AUTHOR = {D’Angelo, Simone and Pagano, Francesca and Caccavale, Riccardo and Scognamiglio, Vincenzo and De Crescenzo, Alessandro and Merone, Pasquale and Ciaravino, Stefano and Finzi, Alberto and Lippiello, Vincenzo},
TITLE = {H-CoRE: A Cooperative Framework for Heterogeneous Multi-Robot Exploration and Inspection},
JOURNAL = {Drones},
VOLUME = {10},
YEAR = {2026},
NUMBER = {4},
ARTICLE-NUMBER = {232},
URL = {https://www.mdpi.com/2504-446X/10/4/232},
ISSN = {2504-446X},
DOI = {10.3390/drones10040232}
}
```

## Architecture Overview

The system consists of several modular ROS2 packages divided into agent-specific Docker environments:

### Ground Control Station (GCS) 
**Repository**: https://github.com/Prisma-Drone-Team/leonardo_managers

The main branch "contest25" contains all the configuration files used for the hardware deploy and the experiments

### UAV agent
**Repository**: https://github.com/Prisma-Drone-Team/uav_motion_stack.git

The branch paper_stable contains modules and instruction for deploying both SITL and specific hardware configurations

### UGV agent

**Repository for Hardware deploy**: https://github.com/Prisma-Drone-Team/Rover-Navigation.git

The main branch contains all the configuration files used for the hardware deploy and the experiments

**Repository SITL Simulation**: https://github.com/Prisma-Drone-Team/rover_sim_motion_stack.git  

Two branches are available: leonardo for stand-alone single robot simulation and multi-robot for multi-robot simulation

### PTZ Camera Agent - Pan-Tilt-Zoom Camera System
**Repository**: https://github.com/Prisma-Drone-Team/ptz_docker_sw  

The branch paper contains modules and instruction for deploying specific hardware configurations

Each repository includes:
- **Single-agent setup**: Standalone operation instructions for individual agent testing
- **Multi-robot integration**: Configuration guidelines for cooperative multi-agent scenarios  
- **Docker deployment**: Containerized environments for reproducible setups
- **Hardware deployment**: Real-world implementation instructions (where applicable)

## Tutorials
H-CoRE framework is fully open-source and available both in plug-and-play simulation and ready to be deployed on actual hardware.

### Available Documentation

- **Complete H-CoRE Simulation Setup**: [`tutorials/sitl_setup.md`](tutorials/sitl_setup.md) - Comprehensive tutorial covering both single-agent and multi-robot simulation environments
- **H-CoRE Hardware Deployment**: [`tutorials/hardware_deployment.md`](tutorials/hardware_deployment.md) - Complete guide for real-world hardware deployment of UAV, UGV, and PTZ agents
- **Individual Agent Setup**: Each repository README provides detailed setup instructions for standalone operation
- **Multi-Robot Coordination**: Integration guidelines available in individual repositories and main tutorials
- **Hardware Deployment**: Real-world implementation instructions in respective agent repositories

The documentation ensures complete reproducibility of experimental setups for both simulation and hardware deployment in research and development environments.
