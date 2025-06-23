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
  - https://medium.com/techmormo/what-is-virtualization-bare-metal-vs-virtual-machines-vs-containers-f3d8be22ad34
  
  - Bare Metal
  - Vitual Machine
    - each VM has its own OS and OS kernel. Which is called Guest OS & Guest OS Kernel.
    - virtualization
      - A Hypervisor is a software that imitates a particular piece of computer hardware or the entire computer
      - allowing the available physical resources to be partitioned into multiple virtual ones, called Virtual Machines (VMs).
      - The computer that runs a hypervisor is called the Host System, and the VMs created and managed by the hypervisor are called the Guest Systems.
      - Hypervisors can sit directly on top of the hardware (type-1) or on top of an OS (type-2)
      - PROBLEM
          - each VM virtualizes an entire operating system and its underlying hardware.
  - Containers
    - Containers virtualize just the operating system, instead of virtualizing the the entire physical machine like VMs.
    - All containers running on a host machine share the OS kernel of the Host System, and only contain the application(s) and their libraries and dependencies.
    - This makes them extremely lightweight & fast!
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
