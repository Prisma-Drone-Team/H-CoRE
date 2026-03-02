# H-CoRE

This repository contains tools and configurations for H-CoRE (Heterogeneous Cooperative multi-Robot Execution) framework simulation and hardware deployment integrated with ROS2 Humble in Docker environments.

<div align="center">
<img src="../figs/logo_prisma.jpg" alt="H-CoRE" width="50%">
</div>

## Article
The description of the single agents' architecture, the software integration, and the framework validation is described in the following article:

Simone D’Angelo*, Francesca Pagano, Riccardo Caccavale, Vincenzo Scognamiglio, Alessandro De Crescenzo, Pasquale Merone, Stefano Ciaravino, Alberto Finzi, and Vincenzo Lippiello, "H-CoRE: A Cooperative Framework for Heterogeneous Multi-Robot Exploration and Inspection"

This work is actually submitted and under review at MDPI - Drones 

## Video
Supplementary video showcasing the proposed framework and the corresponding experimental validation is available at: https://youtu.be/VcLkpbIYOPw

## Developers and License

**Developed by**: Aerial Robotics Group - [PRISMA Lab](https://github.com/prisma-lab), University of Naples Federico II

**Lead Developers**:
- Simone D'Angelo (Corresponding author)
- Francesca Pagano  
- Riccardo Caccavale
- Vincenzo Scognamiglio

**License**: This software is **open-source** and freely available for research and educational purposes. 

**Citation**: If you use this framework in your research, please cite the following paper:

```bibtex
@article{dangelo2024hcore,
  title={H-CoRE: A Cooperative Framework for Heterogeneous Multi-Robot Exploration and Inspection},
  author={D'Angelo, Simone and Pagano, Francesca and Caccavale, Riccardo and Scognamiglio, Vincenzo and De Crescenzo, Alessandro and Merone, Pasquale and Ciaravino, Stefano and Finzi, Alberto and Lippiello, Vincenzo},
  journal={Drones (MDPI)},
  year={2026},
  note={Submitted, under review}
}
```

## Architecture Overview

The system consists of several modular ROS2 packages divided into agent-specific Docker environments:

### Ground Control Station (GCS) 
**Repository**: https://github.com/Prisma-Drone-Team/leonardo_managers

### UAV agent
**Repository**: https://github.com/Prisma-Drone-Team/uav_motion_stack.git

The branch paper_stable contains modules and instruction for deploying both SITL and specific hardware configurations

### UGV agent

**Repository for Hardware deploy**: https://github.com/Prisma-Drone-Team/Rover-Navigation.git

**Repository SITL Simulation**: https://github.com/Prisma-Drone-Team/rover_sim_motion_stack.git  
**Documentation**: Comprehensive navigation stack setup, autonomous exploration algorithms, and multi-robot coordination guidelines

### PTZ Camera Agent - Pan-Tilt-Zoom Camera System
**Repository**: https://github.com/Prisma-Drone-Team/ptz_docker_sw  
**Documentation**: Complete installation and configuration instructions for surveillance and inspection capabilities

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
