# docker-beginner_to_pro
https://www.youtube.com/watch?v=RqTEHSBrYFw&amp;t=2886s

# Prerequisite
- Linux fundamentals - Basic Linux commands

# History & Motivation
- Docker helps to make local env as close as to production env where we are gonna deploy our application.
- setting up development env is easy. Just one command "docker compose up"
- earlier we need "deploment binary(JAR/WAR)", "dependencies", "configurations" to deploy an application. But with containers, just run this container image with these options.
# Technology overview
- containers
  - "lightweight", "standalone", "executable" package of software. This PACKAGE include "everything to run an application".
- Open Container Initiative - OCI
  - defines specification for containers.
    - Runtime specification
      - How you take an image and run it in a container ? 
    - Image specification
      - What format and metadata an image should include?
    - Distribution specification
      - How those images should be distributed.
      - registry, pulling & pushing of the images.
  - Docker, Google, VMWare, Microsoft & Dell has their "own implemention" of this "specification for containers".
- dockers
- Evaluation of Virtualization
  - https://medium.com/@dncgr8/vms-vs-container-191ed90c8019
  - https://erik-engheim.medium.com/containers-vs-vms-a80fe0f9a549
  - https://mkaschke.medium.com/virtual-machine-vm-vs-container-13ab51f4c177
  - https://medium.com/@marco.lindner/kernkonzepte-container-vs-vms-images-container-docker-engine-3eb1e5ac8067
  
  - Bare Metal
      - Bare Metal
  - Vitual Machine
    - each VM has its own Guest OS and it's Kernel through HYPERVISOR ( Type1 or Type2 )
    - Hypervisors can sit directly on top of the hardware (type-1) or on top of an OS (type-2)
    - multiple OS instances run on single host machine.
    - A Hypervisor is a software that imitates a particular piece of computer hardware or the entire computer.
    - Hypervisor allow the available physical resources to be partitioned into multiple virtual ones, called Virtual Machines (VMs).
    - The computer that runs a hypervisor is called the Host System(laptop, server, vm on ec2), and the VMs created and managed by the hypervisor are called the Guest Systems.
    - PROBLEM
          - each VM virtualizes an entire operating system and its underlying hardware.
  - Containers
    - All containers running on a host machine, share the OS kernel of the Host System, and only contain the application(s) and their libraries and dependencies.
    - each container uses Host OS and it's Kernel through Docker Engine.
    - Faster STARTUP, Less RESOURCES (lightweight)
    - Less ISOLATION as compared to VMs.
    - Host OS COMPATIBILITY ISSUE
        - Linux container will run on a Linux host, but not on a Windows host
    - Docker Engine
      - Docker Daemon (`dockerd`): Manages Docker objects such as containers, images, networks, and volumes.
      - REST API: Provides a programmable interface that allows various tools to interact with the Docker daemon.
      - CLI (`docker`): Provides users with a command-line interface for interacting with Docker.
      - Docker Compose : Allows you to define and run multi-container Docker applications.
      - Docker Swarm : A clustering and orchestration tool for Docker containers.
  - In summary, the reduced isolation and dependence on the host OS of containers bring both advantages in terms of performance and efficiency, as well as certain disadvantages, particularly in terms of security and portability. These factors must be considered when deciding whether to use containers or VMs for a particular application.
# Installation / Setup -  Hello World

# Using 3rd Party Containers

# Demo Application

# Building container images
- Dockerfile basics
- Dockerfile optimization
- Buildx + multi-architecture

# Container Registry

# Running Containers

# Container Security

# Interacting with Docker Objects

# Development workflow

# Deploying Containers 
