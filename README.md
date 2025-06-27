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

# Docker networking
- https://www.youtube.com/watch?v=5grbXvV_DSk&t=564s
- https://www.youtube.com/watch?v=bKFMS5C4CG0
- docker creates 3 network driver (network types) automatically.
- 3 "driver" or "network type" is Bridge, None, Host.
- built-in DNS server run on IP 171.17.0.11
    - DNS server will resoLVE CONTAINER_NAME to IP_ADDRESS.
- defualt bridge driver ( network type )
    - default network
        - IP 172.17.0.1 aasigned to interface "docker0"
        - IP 172.17.0.2 aasigned to first container
        - IP 172.17.0.3 assigned to second container
        - and so on...
        - till 172.17.0.16
    - docker run --rm -d redis
    - to access these containers from outside, we need port binding.
        - exposing containers to the world using port binding.
        - docker run --rm -d -P 80:80 redis 
    - Container can be accessed in broswer only if port binding done.
        - http://IP_ADDRESS_OF_HOST_MACHINE:80
    - "docker inspect CONTAINER_ID" OR "docker inspect CONTAINER_NAME"
        - docker inspect redis
        - "redis" is the container name 
        - show "network" of a container. It will be only one.
    - "docker inspect NETWORK_ID" OR "docker inspect NETWORK_NAME"
        - docker inspect bridge 
        - "bridge" is the name of the network.
        - show "all containers" of a network. It can be multiple.
    - "ip a | grep docker0" command
        - Docker create interfaces for every bridge network
        - "docker0" is the interface of the default_bridge network. It IP is 172.17.0.1
    - containers communicate with each other using their internal IP address.
        - CONTAINER_1 - docker run --it -d --name redis-container redis
        - CONTAINER_2 - docker run --it -d --name nginx-container nginx
        - inside CONTAINER_1 (redis-container) IP 172.17.0.2
            - ping 172.17.0.3
            - ping google.com
            - "ip route" command
                - it will show "default via 172.17.0.1" which means routing via interface docker0 ( 172.17.0.1 )
       - inside CONTAINER_2 (nginx-container) IP 172.17.0.3
            - ping 172.17.0.2 
            - ping google.com
        - CHALLENGE
            - our application(container) want to connect to database (container).
            - after container restart, new IP address will be assiged, so communication using IPs is not correct.
        - SOLUTION
          - "user-defined" Bridge  
              - "user-defined" network is isolated from all other networks ( default, none & host). can't talk to them.
              - docker network create --driver bridge --subnet 182.8.x.x/16 custom-isolated-network
              - "custom-isolated-network" is the name of the user-defined network.
              - containers of this network communicate with each other using NAMES.
                  - mysql.connect(CONTAINER_NAME)
                  - CONTAINER_1 - docker run --it -d --name redis-container -net user-defined-network redis
                  - CONTAINER_2 - docker run --it -d --name nginx-container -net user-defined-network nginx
                  - inside CONTAINER_1 (redis-container) IP 172.17.0.2
                      - ping nginx-container
                      - ping google.com
                      - "ip route" command
                          - it will show "default via 172.17.0.1" which means routing via interface docker0 ( 172.17.0.1 )
                   - inside CONTAINER_2 (nginx-container) IP 172.17.0.3
                        - ping redis-container 
                        - ping google.com 
                    - we can attach a network to a cotainer as part of the "docker run" command.
                    - docker run --net custom-isolated-network --it redis
                    - from inside container, we can execute "ping google.com" OR "ping HOST_MACHINE_IP_ADDRESS"
                    - but we cannot ping any IP address of the "default" bridge network due to isolation. ping 172.17.0.2 , won't work.
                    - we can also ping CONTAINER1 from CONTAINER2 or vice-versa. Both containers are attached to the same "user-defined" bridge network.
              - "docker network ls" command show all networks with details like NETWORK_ID, NAME, DRIVER & SCOPE
              - "ip a | NETWORK_ID" command
                  - show "network interface" details as each network has its own interface.
                  - IPs of "user-defined" bridge network is different than "default" bridge network.


- Host
    - docker run redis --network host
    - ZERO isolation between container & host.
    - "container wants to connect to other resources/servicrs on the host"
    - "this container is like any other application directly deployed on the host without the docker"
    - "just like a regular application on the host"
    - we don't need to expose the port.
    - container uses the network of the host machine.
    - multiple container cannot be run on the same port.
- overlay network
    - create private overlay network across multiple hosts of a Docker swarm.
    - docker network --driver overlay --subnet 10.0.9.0/24 create my-overlay-network
    - create network across multiple host machines.
    - host1(container1, container2), host2(container3, container4), host3(container5, container6) are 3 different networks.
- ingress network
    -  
- None = docker run redis --network none
    - container is not attached to any network.
    - does not have any access to external network or any other container.
    - run in an isolated network.



   
 

# Container Security

# Interacting with Docker Objects

# Development workflow

# Deploying Containers 
